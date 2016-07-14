---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Dernières mises à jour apportées au pack de construction sdk-for-nodejs
{: #latest_updates}

*Dernière mise à jour : 22 juin 2016*
{: .last-updated}

Liste des dernières mises à jour apportées au pack de construction sdk-for-nodejs.
## 22 juin 2016 : Pack de construction Node.js v3.5-20160608-1102 mis à jour

Cette édition du pack de construction ajoute l'environnement d'exécution IBM SDK for Node.js, versions 4.4.5 et 6.2.0. La valeur par défaut devient 4.4.5.

L'édition retire la prise en charge des anciennes versions de l'environnement d'exécution, comme annoncé dans [Bluemix Node.js Buildpack v3.3 – FIPS mode and more](https://developer.ibm.com/bluemix/2016/05/05/node-buildpack-update-fips-mode/). L'environnement d'exécution prend désormais en charge les versions 0.10.44, 0.10.45, 0.12.13, 0.12.14, 4.4.4, 4.4.5, 6.1.0 et 6.2.0.

Cette édition inclut les correctifs de bogue provenant du [pack de construction Node.js 1.5.14 de Cloud Foundry](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.14).

## 20 mai 2016 : Pack de construction Node.js v3.4-20160518-1653 mis à jour

Cette édition du pack de construction ajoute l'environnement d'exécution IBM SDK for Node.js, versions 0.10.45, 0.12.14, 4.4.4, 6.0.0 et 6.1.0. La version par défaut est désormais 4.4.4. 

Des correctifs sont inclus pour les vulnérabilités en matière de sécurité suivantes :
* [CVE-2015-8855](http://www-01.ibm.com/support/docview.wss?uid=swg21982852)
* [CVE-2016-2108 CVE-2016-2107 CVE-2016-2105 CVE-2016-2106 CVE-2016-2109 CVE-2016-2176](https://www.openssl.org/news/secadv/20160503.txt)

Notez qu'il s'agit d'un problème connu lié à npm v3 et à l'utilitaire App Management Inspector. npm 3.8.6 est la version par défaut avec les environnements d'exécution 6.0.0 et 6.1.0. Si vous souhaitez utiliser l'un des environnements d'exécution 6.x et l'utilitaire Inspector, vous devez spécifier une version npm 2.x dans votre fichier package.json comme solution temporaire. 

## 29 avril 2016 : Pack de construction Node.js v3.3-20160428-1409 mis à jour

Cette édition du pack de construction ajoute l'environnement d'exécution IBM SDK for Node.js, versions 0.10.44, 0.12.13, 4.4.0, 4.4.1, 4.4.2 et 4.4.3. La valeur par défaut est désormais 4.4.3.
Pour la version 4.3.1 et les versions ultérieures, il est désormais possible d'utiliser une version compatible FIPS de l'environnement d'exécution en définissant la variable d'environnement `FIPS_MODE=true` pour votre application. 

Le pack de construction mis à jour et les nouvelles versions d'environnement d'exécution contiennent aussi des correctifs relatifs aux vulnérabilités en matière de sécurité :
* [CVE-2016-2515](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-2537](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-3956](http://www-01.ibm.com/support/docview.wss?uid=swg21980827)

Le pack de construction mis à jour contient également des correctifs pour plusieurs bogues :
* IBM SDK for Node.js sera toujours utilisé si une version qui correspond à la plage requise est disponible. Auparavant, cela n'était vrai que pour les versions d'environnement d'exécution 4.x.
* L'utilitaire App Management Inspector fonctionne désormais avec les versions d'environnement d'exécution 4.x.
* Une régression a été corrigée dans l'utilitaire strongpm App Management. 

## 18 mars 2016 : Pack de construction Node.js v3.2-20160315-1257 mis à jour

Cette édition du pack de construction déplace l'environnement d'exécution IBM SDK for Node.js par défaut de la version 4.3.0 vers la version 4.3.2. Elle comprend également IBM SDK for Node.js versions 0.10.43, 0.12.12 et 4.3.1. Utilisez ces versions Node.js récentes pour récupérer les correctifs relatifs à plusieurs vulnérabilités en matière de sécurité. 

## 4 mars 2016 : Pack de construction Node.js v3.1-20160222-1123 mis à jour

Cette édition du pack de construction déplace l'environnement d'exécution IBM SDK for Node.js par défaut de la version 4.2.4 vers la version 4.3.0. Elle comprend également IBM SDK for Node.js versions 0.10.42, 0.12.10 et 4.2.6. Utilisez ces versions Node.js récentes pour récupérer les correctifs relatifs à plusieurs vulnérabilités en matière de sécurité. 

## 4 février 2016 : Pack de construction Node.js v3.0-20160125-1224 mis à jour

Cette édition est totalement synchronisée avec le pack de construction [Cloud Foundry community Node.js](https://github.com/cloudfoundry/nodejs-buildpack). En plus des modifications de communauté, certaines valeurs par défaut ont été modifiées, certaines optimisations ont été effectuées afin réduire le temps de transfert, et des mises à jour ont été apportées à la fonction App Management.

* Mises à jour du pack de construction :

  * Node.js v4.2.4 (IBM SDK for Node.js version 4) est désormais l'environnement d'exécution par défaut sur Bluemix ; il remplace la version v0.12.9. Par conséquent, il se peut que votre application se comporte différemment si vous n'avez pas indiqué une version spécifique pour celle-ci. Pour savoir comment spécifier une version de Node.js pour votre application Bluemix, voir la documentation de l'[environnement d'exécution Node.js](index.html).

  * Désormais, NODE_ENV prend la valeur par défaut *production*. Cela va modifier le comportement de certaines dépendances de noeud. Par exemple, l'infrastructure Express ne renverra plus de traces de piles dans le navigateur Web pour les noeuds finaux en erreur, mais affichera un message signalant une *erreur de serveur interne*. Lorsque NPM_CONFIG_PRODUCTION aura pour valeur *true*, NPM affectera à NODE_ENV la valeur *production* pour les scripts de sous-interpréteur de commandes lors de la phase d'installation de npm uniquement. Cela permettra aux utilisateurs d'affecter une autre valeur à NODE_ENV, par exemple, *development*, pour l'environnement d'exécution d'application. Pour plus de clarté, les scripts npm visualiseront le message **NODE_ENV=production**.

  * Un correctif de bogue pour le service Monitoring and Analytics est inclus.

* Mises à jour apportées à la mise en cache :

  * Si la mise en cache est désactivée (NODE_MODULES_CACHE=false), le pack de construction ne tentera pas de mettre en cache des modules/composants. Auparavant, ce paramétrage était tel que la mise en cache ne s'affichait pas, mais les modules installés étaient tout de même mis en cache en vue d'un déploiement ultérieur. Aujourd'hui, la mise en cache ne s'affiche pas et aucune tentative de mise en cache n'est effectuée.

  * Les composants Bower_components sont mis en cache par défaut en plus des modules node_modules.

* Autres mises à jour :

  * Des avertissements utiles ont été ajoutés pour signaler des dépendances manquantes, telles que gulp, bower et angular.

  * La détection de scripts est mise à jour avec les informations de version du pack de construction.

  * La recommandation relative au groupement (WEB_CONCURRENCY) initialement présentée par la communauté a été retirée, car la détermination de la mémoire était inexacte sur Bluemix.


## 16 décembre 2015 : Pack de construction Node.js v2.8-20151209-1403 et v3.0beta-20151211-2041 mis à jour

Cette édition du pack de construction Node.js est livrée avec deux versions, la version 2.0 et la version 3.0 bêta. Elles incluent toutes les deux les
modifications suivantes :

Correctif de bogue pour le service Monitoring and Analytics. Inclusion d'un environnement d'exécution en cache pour IBM SDK for Node.js v4.2.3.0, v4.2.2.0, v1.2.0.8 et v1.2.0.7 (versions basées sur les versions Node.js v4.2.3, v4.2.2, v0.12.9 et v0.12.8 de la communauté). En outre, dans la version 3.0 bêta, l'environnement d'exécution Node.js par défaut est passé à v4.2.3.

Le pack de construction IBM Node.js version 3.0 bêta est désormais publié en tant que pack de construction autre que le pack de construction par défaut dans
Bluemix, avec Node.js
version 4.2.3 comme environnement d'exécution par défaut. Pour garantir le fonctionnement de vos applications et de vos services dans Bluemix, envoyez par
commande push votre application avec la version bêta du pack de construction. Après 30 jours ou plus, la version 3 deviendra le pack de construction par
défaut.

Pour envoyer par commande push votre application avec la version 3.0 bêta :
* Utilisez l'option "-b" dans votre commande 'cf push' :

```
        cf push -b sdk-for-nodejs-v3beta
```
{: codeblock}

* Ou, utilisez l'option "buildpack" dans votre fichier manifest.yml :

```
        buildpack: sdk-for-nodejs-v3beta
```
{: codeblock}

Le passage à l'environnement d'exécution par défaut n'a pas d'impact sur votre application si vous avez configuré une version spécifique de Node.js dans le
fichier package.json de votre application. **Remarque :** Vous pouvez toujours spécifier la version de Node.js pour l'exécution de votre application à l'aide de l'entrée
engines.node de votre fichier package.json, comme expliqué dans [Versions disponibles](index.html#available_versions).

## 23 novembre 2015 : Pack de construction Node.js v2.7-20151118-1003 mis à jour

Avec la version 2.7, la version 4.2.1.0 d'IBM SDK for Node.js (reposant sur Node version 4.2.1 LTS) est incluse. Il ne s'agit pas encore de la version par défaut, mais elle peut être spécifiée en vue de son utilisation. **Remarque :** Cette version remplace la construction open source précédemment disponible. Nous avons également appliqué quelques petits correctifs de bogue à notre infrastructure d'extension de service.

## 19 octobre 2015 : Pack de construction Node.js v2.6.1-20151015-1326 mis à jour

Node.js version 2.6.1 introduit un correctif de bogue pour le
[gestionnaire StrongPM
d'App Management](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/) ainsi qu'une version NPM plus cohérente.

## 15 octobre 2015 : Pack de construction Node.js v2.6-20151006-1309 mis à jour

Cette édition du pack de construction Node.js contient l'intégration de [StrongLoop
Process Manager](https://strong-pm.io) à la fonction App Management. Pour plus d'informations, voir l'article de blogue [StrongLoop DevOps for Node.js Applications on Bluemix](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/).

## 15 juin 2015 : Pack de construction Node.js v2.0-20150608-1503 mis à jour

Dans cette édition, nous avons synchronisé notre pack de construction Node.js avec le
[pack de construction Node.js de la communauté CF](https://github.com/cloudfoundry/nodejs-buildpack) le
plus récent, qui est livré avec plusieurs nouvelles fonctions apportées par la communauté.
De plus, nous avons réorganisé la fonction App Management du pack de construction Node.js, qui active des utilitaires tels que le shell,
node-inspector, Bluemix Live Sync, etc. Voir [App Management](../../manageapps/app_mng.html) pour plus de détails.

## 5 mai 2015 : Pack de construction Node.js v1.17-20150429-1033 mis à jour

* Désormais, le pack de construction Node.js est livré avec
[IBM SDK for Node.js
version 0.12.1](https://developer.ibm.com/node/sdk/).
* Si le fichier package.json de votre application ne spécifie pas d'environnement d'exécution, l'application démarre désormais avec la version 0.12.1 au lieu de
la version 0.10.x. Si vous avez besoin d'utiliser la version précédente, spécifiez la version 0.10.x dans votre fichier package.json,
de la façon suivante :

```
        "engines": {
            "node": "0.10.x"
        }
```
{: codeblock}

* Problèmes connus liés à la version 0.12.1 :
   * La fonction "Suspend" ne fonctionne pas lorsque vous utilisez la fonction Debug Tools mise à disposition par Bluemix Live Sync. 
   * Le module mqlight utilisé pour le service MQ Light n'est pas pris en charge dans la version 0.12.x.

* Diverses vulnérabilités de sécurité ont été résolues :
  * Des vulnérabilités dans OpenSSL affectant IBM SDK for Node.js ont été corrigées. Vous trouverez plus de détails dans le
[bulletin de sécurité](http://www-01.ibm.com/support/docview.wss?uid=swg21701494).
  * Vulnérabilités corrigées dans le chiffrement de flux RC4 affectant IBM SDK for Node.js. Vous trouverez plus de détails dans le
[bulletin de sécurité](http://www-01.ibm.com/support/docview.wss?uid=swg21882778).

##  2 avril 2015 : Pack de construction Node.js v1.15-20150331-2231 mis à jour

* Désormais, le pack de construction Node.js inclut trois nouvelles fonctions qui permettent de développer des applications rapidement dans Bluemix, comme vous le feriez
sur le bureau, sans avoir à les redéployer.
  * Desktop Sync : synchronisez une arborescence de bureau (Windows) avec un espace de travail de projet reposant sur un cloud.
  * Live Edit : vous pouvez apporter des modifications à une application Node.js qui s'exécute dans Bluemix et les tester immédiatement dans votre navigateur.
  * Debug : ouvrez un shell dans votre environnement et procédez au débogage. Vous pouvez éditer le code dynamiquement, insérer des points d'arrêt, parcourir le
code, redémarrer l'environnement d'exécution et effectuer d'autres opérations à l'aide du débogueur Node Inspector.
  * Voir [App Management](../../manageapps/app_mng.html#Utilities) pour plus d'informations.
* Nous avons extrait les modifications les plus récentes du [pack de construction Node.js de Cloud Foundry](https://github.com/cloudfoundry/nodejs-buildpack). Ces modifications sont fournies avec plusieurs correctifs de bogue et améliorations apportés par la communauté.
* Désormais, le pack de construction Node.js est livré avec
[IBM SDK for Node.js
version 1.1.0.13](https://developer.ibm.com/node/sdk/).

## 5 janvier 2015 : Pack de construction Node.js v1.9.1-20141208-1221 mis à jour

* Désormais, le pack de construction Node.js prend en charge le paramétrage dynamique des journaux. Ainsi, les développeurs peuvent changer le niveau de
journalisation de leur application de manière dynamique si l'application utilise le module log4js, bunyan ou ibmbluemix pour la journalisation.
* Désormais, le pack de construction Node.js est livré avec
[IBM SDK for Node.js
version 0.10.33](https://developer.ibm.com/node/sdk/). Cette mise à jour inclut des correctifs pour le problème POODLE. 

## 23 octobre 2014 : Pack de construction Node.js v1.6-20141013-1736 mis à jour

* Désormais, le pack de construction Node.js est livré avec
[IBM SDK for Node.js
version 1.1.0.8](https://developer.ibm.com/node/sdk/). Cette mise à jour signifie que vous obtenez un environnement d'exécution
IBM Node.js entièrement pris en charge
lorsque vous indiquez l'environnement d'exécution Node.js stable le plus récent
pour votre application, à savoir la version 0.10.32. Ce logiciel SDK le plus récent
contient un correctif visant à résoudre un problème du module qs imbriqué
qui entraînait un refus de service. Il contient également une version mise à jour du module npm, ainsi que d'autres
améliorations apportées aux modules http et url. Pour plus de détails, voir le [journal des modifications de la version 0.10.32](https://raw.githubusercontent.com/joyent/node/v0.10.32/ChangeLog).
* Le pack de construction contient aussi un correctif visant à résoudre un
bogue qui ajoutait un fichier index.html incorrect dans l'application du
client pendant le déploiement.

## 30 septembre 2014 : Pack de construction Node.js v1.4-20140908-1746 mis à jour

* Désormais, le pack de construction Node.js est livré avec [IBM SDK for Node.js version 1.1.0.7](https://developer.ibm.com/node/sdk/). Cette mise à jour signifie que vous obtenez un environnement d'exécution
IBM Node.js entièrement pris en charge
lorsque vous indiquez l'environnement d'exécution Node.js stable le plus récent
pour votre application, à savoir la version 0.10.31. Avec un environnement d'exécution Node.js entièrement pris en charge, les clients bénéficient d'une expérience de prise en charge cohérente. 
* Le pack de construction contient une infrastructure de service améliorée. Plus spécifiquement, elle fonctionne mieux lors de la liaison du service Monitoring and Analytics et fournit des informations de diagnostic supplémentaires en cas d'échec du service.

## 28 août 2014 : Pack de construction Node.js v1.3-20140821-1143 mis à jour

* Le pack de construction Node.js le plus récent est livré avec IBM SDK for Node.js version 1.1.0.6. Cette mise à jour signifie
que vous disposez d'un environnement d'exécution IBM Node.js entièrement pris en charge lorsque vous spécifiez l'environnement d'exécution Node.js stable le plus récent, à savoir la version 0.10.30, pour votre application. Cet environnement d'exécution corrige la
[vulnérabilité à l'altération de la mémoire dans la version 8](http://blog.nodejs.org/2014/07/31/v8-memory-corruption-stack-overflow).
* Ce pack de construction comprend également des améliorations et des correctifs de bogue concernant l'extension de service Monitoring and Analytics, et vous permet
d'effectuer un diagnostic des performances et des conditions d'erreur via le service.

## 29 juillet 2014 : Pack de construction Node.js v1.1-20140717-1447 mis à jour

Désormais, le pack de construction Node.js est livré avec IBM SDK for Node.js version 1.1.0.5. Cette mise à jour signifie que vous disposez d'un contexte d'exécution
IBM Node.js entièrement pris en charge lorsque vous spécifiez l'environnement d'exécution Node.js
stable le plus récent, à savoir la version 0.10.29, pour votre application. Pour plus d'informations sur les logiciels IBM SDK pour Node.js, cliquez [ici](https://developer.ibm.com/node/sdk/).

# rellinks
{: #rellinks}
## general
{: #general}
* [Contexte d'exécution node.js](index.html)
