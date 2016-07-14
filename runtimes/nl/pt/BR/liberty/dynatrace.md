---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Usando o Dynatrace
{: #using_dynatrace}

*Última atualização: 10 de junho de 2016*
{: .last-updated}

Dynatrace é um serviço de terceiro que fornece monitoramento para seu app.

Para obter mais informações sobre o que o serviço Dynatrace fornece, veja [Monitoramento de aplicativos Dynatrace](http://www.dynatrace.com/en/products/application-monitoring.html).

Quando seu aplicativo Liberty é configurado para usar o Dynatrace, o comportamento
padrão é o tempo de execução do Liberty adquirir um arquivo jar do agente Dynatrace em
um site do Dynatrace e executar esse agente Dynatrace com seu app. Com esse
comportamento padrão, a configuração mínima necessária para usar o Dynatrace é criar um
serviço fornecido pelo usuário que aponte para o coletor Dynatrace.

## Criando um serviço fornecido pelo usuário que aponta para o coletor Dynatrace

Em primeiro lugar, você precisará configurar um coletor Dynatrace. Em seguida,
deve-se criar um serviço fornecido pelo usuário para passar as informações do agente
Dynatrace para conexão com o coletor Dynatrace. Veja [Arquitetura do Dynatrace](https://community.dynatrace.com/community/display/DOCDT63/Architecture) para entender melhor o relacionamento entre os componentes do Dynatrace.

<ol>
<li>Configure um coletor Dynatrace.
  <ul>
  <li>Consulte o [Website da comunidade do Dynatrace](https://community.dynatrace.com/community/display/EVAL/Step+3+-+Connect+Agent+to+Dynatrace) para obter instruções sobre como fazer download e configurar o coletor Dynatrace.
  </li>
  <li>Assegure-se de que o coletor esteja configurado em um local que seja acessível ao agente Dynatrace em execução com seu app no Bluemix.
  </li>
  </ul>
</li>
<li>Crie um serviço fornecido pelo usuário que aponte para o coletor Dynatrace em execução. <b>NOTA</b> O nome do serviço fornecido pelo usuário deve conter <b>dynatrace</b>.  Por exemplo, use o comando que segue:

  <pre>
  $ cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring"}'
  </pre>
  {: codeblock}

Neste exemplo, my-dynatrace-collector é o nome fornecido ao serviço, DynatraceCollectorIPaddress é o endereço IP do coletor Dynatrace configurado por você e profile é o nome do perfil Dynatrace opcional associado a esse app monitorado. O valor do perfil padrão é Monitoring. É possível especificar parâmetros opcionais, como no exemplo que segue.

  <pre>
  $ cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring",
                                        "options" : {"dynatrace-parameter-1": "value",
                                                     "dynatrace-parameter-2": "value"}}'
  </pre>
  {: codeblock}

Veja [Seção Configuração do agente em Configuração do agente](https://community.dynatrace.com/community/display/DOCDT62/Agent+Configuration) no website do comunidade do Dynatrace para obter mais informações sobre as opções disponíveis. Por exemplo, usando a opção exclude, é possível excluir classes de serem monitoradas pelo Dynatrace. Veja [Estrutura do agente DynaTrace](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/framework-dynatrace-agent.md) para obter mais detalhes sobre como configurar o serviço fornecido pelo usuário.
</li>
<li>Depois de ter enviado por push seu app para o Bluemix, ligue o serviço fornecido pelo usuário que você criou ao app. Por exemplo, use o comando

  <pre>
  $ cf bs myApp my-dynatrace-collector
  </pre>  
  {: codeblock}

**Nota**: deve-se remontar o aplicativo após a ligação do serviço.
</li>
</ol>

## Configuração opcional
{: #optional_configuration}

Você pode optar por adquirir e hospedar você mesmo o arquivo jar do agente
Dynatrace. Nesse caso, são necessárias as etapas adicionais de configuração a seguir.
1. Adquira e hospede o arquivo jar do agente Dynatrace para que o buildpack do Liberty possa fazer download dele.
2. Configure seu app Liberty para que ele possa fazer download do agente Dynatrace.

### Hospedando o agente Dynatrace
{: #hosting_dynatrace_agent}
O agente Dynatrace deve ser hospedado em um servidor da web e o buildpack do Liberty deve ser capaz de fazer download do jar do agente a partir desse servidor. O servidor deve ser configurado com um arquivo index.yml que especifica os detalhes sobre o jar do agente. Conclua as etapas a seguir para configurar o agente Dynatrace:
  1. Faça download do jar do agente Dynatrace. Veja [Instaladores da plataforma do servidor Dynatrace](https://community.dynatrace.com/community/display/EVAL/Step+1+-+Download+and+install+Dynatrace) no website da comunidade do Dynatrace para obter instruções sobre como fazer download do jar do agente Dynatrace. O
arquivo jar do agente apropriado para execução no Bluemix é o
**dynatrace-agent-unix.jar** versão **6.+**.
  2. Hospede o arquivo jar do agente em um local a partir do qual o buildpack do Liberty possa fazer download dele. É possível hospedá-lo no próprio Bluemix, usando qualquer um dos recursos do servidor disponível ou hospedá-lo em algum local publicamente disponível.
     * Assegure-se de fornecer um arquivo index.yml no local de hosting. O arquivo index.yml deve conter uma entrada que consiste no ID da versão do jar do agente, seguido por dois-pontos e a URL completa do local desse jar do agente. Por exemplo:
```
      ---
      6.3.0: https://my-dynatrace-agent.mybluemix.net/dynatrace-agent-6.3.0-unix.jar
```  
{: codeblock}
     * O arquivo **dynatrace-agent-6.3.0-unix.jar** deve estar disponível no local especificado no arquivo index.yml. O local para o arquivo jar e o index.yml pode ser o mesmo diretório.

### Configurando o app Liberty
{: #configuring_liberty_app}

O app Liberty que você deseja monitorar deve ser configurado para localizar o servidor que hospeda o jar do agente configurado anteriormente. É possível configurar o app com a variável de ambiente **JBP_CONFIG_DYNATRACEAGENT**. A variável de ambiente **JBP_CONFIG_DYNATRACEAGENT** instrui o buildpack a partir de onde fazer download do agente Dynatrace. Para configurar a variável de ambiente, conclua estas etapas:
<ol>
   <li> Configure a variável **JBP_CONFIG_DYNATRACEAGENT** para que tenha o valor
   *"repository_root: URL_of_server_hosting_index.yml"*. Por exemplo, depois de enviar por push seu aplicativo, emita o comando a seguir:
  
  <pre>   
    $ cf se myApp JBP_CONFIG_DYNATRACEAGENT 'repository_root: https://my-dynatrace-agent-host.mybluemix.net'
  </pre>
  {: codeblock}

  Neste exemplo, *my-dynatrace-agent-host.mybluemix.net* é a URL do arquivo index.yml hospedado pelo servidor configurado anteriormente.
  </li>
  <li> Depois de configurar a variável de ambiente, remonte seu app. O staging_task.log para seu app Liberty emite uma mensagem indicando download bem-sucedido do agente Dynatrace a partir do servidor hosting do agente. Por exemplo:

  <pre>
    Fazendo download do dynatrace-agent-6.3.0-unix.jar 6.3.0 a partir de https://my-dynatrace-agent-host.mybluemix.net/dynatrace-agent-6.3.0-unix.jar (17.8s)
  </pre>
  {: codeblock}

</li>
<li>Para ver o staging_task.log, emita o comando a seguir:

  <pre>
    $ cf files myAppName logs/staging_task.log
  </pre>  
  {: codeblock}

</li>
</ol>

# rellinks
{: #rellinks}
## geral
{: #general}
* [Tempo de execução do Liberty](index.html)
* [Visão geral do perfil do Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
