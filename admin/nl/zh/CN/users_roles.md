---



copyright:

  years: 2015, 2016



---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# 管理团队成员和角色
{: #userroles}
*上次更新时间：2016 年 6 月 1 日*
{: .last-updated}

在您帐户的**团队目录**页面中，可以管理现有团队成员及其在您组织和空间中的角色，还可以邀请新的团队成员。要访问您帐户的团队目录，请转至**帐户和支持**图标 ![“帐户和支持”图标](../admin/images/account_support.svg) &gt; **帐户** &gt; *your_account_name* &gt; **团队目录**。
{:shortdesc}

帐户所有者对组织和空间执行所有操作，包括管理团队成员及其分配的角色。组织管理员有权邀请团队成员并管理角色。空间管理员可以使用**管理组织**页面将现有帐户成员添加到空间，并调整这些成员的角色。请参阅以下信息以了解有关角色的更多信息。

## 角色
{: #userrolesinfo}

在帐户级别，有两个角色支持访问不同的帐户管理功能：

*表 1. 帐户角色和许可权*

| 帐户角色 | 许可权 |    
|----------------|---------|
|所有者 | 帐户所有者有权访问其个人档案、团队目录、记帐信息、花费通知和使用情况仪表板。在“团队目录”页面中，所有者可以邀请新的团队成员并调整角色。所有者还可以添加促销信贷，设置或更改记帐限制，设置服务访问权以及管理组织和空间。 |
|成员 | 成员有权在 {{site.data.keyword.Bluemix_notm}} 标题中访问其个人档案、团队目录、帐户信贷和记帐限制。但是，在“团队目录”页面上，成员只能查看该帐户内的团队成员。 |

 所有新的团队成员都会添加为该帐户的成员。您可以为被邀请者添加组织和空间角色，以在 {{site.data.keyword.Bluemix_notm}} 中启用特定视图和许可权。缺省情况下，会向添加到组织的新团队成员分配审计员组织角色。对于特定空间，可以选择向被邀请者分配开发者或审计员角色。一旦被邀请者接受邀请并加入 {{site.data.keyword.Bluemix_notm}}，您就可以在**团队目录**页面上编辑这些被邀请者的角色。

可以在组织级别分配以下角色：

*表 2. 组织角色和许可权*

| 组织角色 | 许可权 |    
|-------------------|-------------|
|管理器 | 组织管理员可以创建、查看、编辑或删除组织内的空间，查看组织的使用情况和配额，邀请团队成员加入组织，管理谁有权访问组织及其在组织中的角色，以及管理组织的定制域。 |
|记帐管理员 | 记帐管理员可以在“使用情况仪表板”页面上查看组织的运行时和服务使用情况信息。  |
|审计员 | 组织审计员可以查看组织中的应用程序和服务内容。审计员还可以查看组织中的团队成员及其分配的角色，以及组织的配额。缺省情况下，会向所有被邀请者分配此角色。|

可以在空间级别分配以下角色：

*表 3. 空间角色和许可权*

| 空间角色 | 许可权 |    
|------------|-------------|
|管理器 | 空间管理员可以添加现有团队成员，并管理空间内的角色。空间管理员还可以查看空间中每个应用程序的实例数、服务绑定和资源使用情况。 |
|开发者 | 空间开发者可以创建、删除和管理空间内的应用程序和服务。某些管理任务包括部署应用程序，启动或停止应用程序，重命名应用程序，删除应用程序，重命名空间，将服务绑定到应用程序或从应用程序取消绑定服务，以及查看空间中每个应用程序的实例数、服务绑定和资源使用情况。此外，空间开发者还可以将内部或外部 URL 与空间中的应用程序相关联。   |
|审计员 | 空间审计员具有对有关空间的所有信息的只读访问权，例如有关空间中每个应用程序的实例数、服务绑定和资源使用情况的信息。 |

**注**：分配有管理者或开发者空间角色的团队成员可以访问 VCAP_SERVICES 环境变量。但是，分配有审计员角色的团队成员无法访问 VCAP_SERVICES。

## 邀请团队成员
{: #inviteteammembers}

帐户所有者和组织管理员可以在“邀请团队成员”页面中邀请团队成员加入组织。添加新的团队成员时，会自动向其分配审计员角色。您可以日后在“团队目录”页面上更改这些角色。要邀请团队成员，请完成以下步骤：

<ol>
<li>转至**帐户和支持**图标 ![“帐户和支持”图标](../admin/images/account_support.svg) &gt; **帐户** &gt; *your_account_name* &gt; **邀请团队成员**。</li>
<li>选择要邀请团队成员加入的组织。</li>
<li>单击**下一步**。</li>
<li>选择要允许团队成员访问的空间。</li>
<li>选择要为组织中所选空间分配的角色。</li>
<li>选择相应选项以确认您负责支付该帐户发生的所有费用。</li>
<li>输入单个团队成员的电子邮件地址，或输入多个团队成员的电子邮件地址：
<ul>
<li>要添加单个团队成员，请输入电子邮件地址，然后单击**发送**。</li>
<li>要添加多个团队成员，请单击**同时邀请所有人**。输入使用逗号、空格或换行符分隔的电子邮件地址列表。接着，单击**下一步**以验证要向其发送邀请的电子邮件地址，然后单击**发送**。</li>
</ul>
</li>
</ol>

单击**查看暂挂**以检查邀请是处于暂挂状态还是已被接受。可以随时选择重新发送邀请电子邮件或对暂挂邀请取消邀请。

如果您具有与 {{site.data.keyword.Bluemix_notm}} 帐户相链接的 SoftLayer 帐户，那么您可以添加 SoftLayer 团队成员。转至**帐户和支持**图标 ![“帐户和支持”图标](../admin/images/account_support.svg) &gt; **帐户** &gt; *your_account_name* &gt; **邀请团队成员**页面。然后，在**添加 SoftLayer 团队成员**部分中单击**添加**，以在 SoftLayer 帐户中进行认证，并查看 SoftLayer 帐户的团队成员列表。有关从 SoftLayer 帐户添加团队成员的更多信息，请参阅[邀请 SoftLayer 团队成员加入 {{site.data.keyword.Bluemix_notm}}](../admin/softlayerlink.html#invite_users)。

## 编辑角色
{: #editinguserroles}

帐户所有者和组织管理员可以在**团队目录**页面上编辑现有团队成员的组织和空间角色。 

1. 转至**帐户和支持**图标 ![“帐户和支持”图标](../admin/images/account_support.svg) &gt; **帐户** &gt; *your_account_name* &gt; **团队目录**。
2. 找到要编辑其角色的团队成员。
3. 单击**查看角色**。
4. 选择或清除组织角色选项，以修改团队成员的组织访问权。
5. 单击**查看空间**以添加或除去空间角色。
6. 选择或清除空间角色选项，以修改团队成员的空间访问权。
7. 单击**关闭空间**。
8. 单击页面末尾的**保存**。

空间管理员可以在**管理组织**页面上编辑其空间中团队成员的角色。

1. 转至**帐户和支持**图标 ![“帐户和支持”图标](../admin/images/account_support.svg) &gt; **帐户** &gt; *your_account_name* &gt; **管理组织**。
2. 找到您的空间所在的组织。
3. 单击**查看详细信息**。
4. 找到您的空间，然后单击**编辑空间**。
5. 选择**用户**选项卡。
6. 对于要为团队成员添加或除去的角色，选择或清除空间角色选项。
7. 单击**保存**。