Módulo WHMCS para Node
=========

Cliente API Node para WHMCS.

## Pré-requisitos

Instale o [Node.js](https://nodejs.org/en/) versão 18.0.0 ou superior.

## Instalação


```
npm install whmcs
```

## Uso

Primeiro, você precisa instanciá-lo.

Você pode instanciar com credenciais da API:

```javascript
const config = {
  apiIdentifier: '<seu_identificador_api>',
  apiSecret: '<seu_segredo_api>',
  accesskey: '<sua_chave_de_acesso>', //opcional. use isso para ignorar restrições de IP
  serverUrl: 'http://127.0.0.1',
  userAgent: '<seu_agente_de_usuario>'
};

const wclient = new WHMCS(config);

Ou você pode instanciar com nome de usuário do administrador e senha MD5 hash:

```javascript
const config = {
  username: process.env.WHMCS_USER || '<seu_nome_de_usuário_admin>',
  password: process.env.WHMCS_PASSWORD || '<sua_senha_hash_md5>',
  accesskey: '<sua_chave_de_acesso>', //opcional. use isso para ignorar restrições de IP
  serverUrl: 'http://127.0.0.1',
  userAgent: '<seu_agente_de_usuario>'
};

const whmcs = new WHMCS(config);
```

Com o cliente WHMCS criado, você deve obter a categoria/módulo desejado (veja os módulos disponíveis) e chamar o método necessário.

Por exemplo, você pode buscar 10 usuários assim:

```javascript
const parameters = {
  limitstart: 0,
  limitnum: 10
};
  
whmcs.users.getUsers(parameters)
  .then(details => {
    ...
  })
  .catch(err => {
    ...
  });
```

Se desejar/necessitar, você pode usar callbacks em vez disso:

```javascript
const parameters = {
  limitstart: 0,
  limitnum: 10
};
  
whmcs.users.getUsers(parameters, function (err, details) {
  ...
});
```

## Arquitetura do Módulo

Este módulo node-js segue a estrutura do Índice da API WHMCS, que possui funções organizadas por categorias. Cada categoria é representada aqui por um objeto de módulo, e cada módulo possui métodos públicos representando as funções da WHMCS.
<br/>
Quando a função da WHMCS requer parâmetros, eles devem ser agrupados em um objeto JSON e então podem ser definidos como o primeiro argumento do método. Se nenhum parâmetro for necessário, este argumento não deve ser definido. O argumento "callback" é opcional, e quando não fornecido, o método retorna uma Promise. Este padrão é compartilhado em todos os métodos públicos dos módulos.
<br/>

## Funções implementadas

O Índice da API WHMCS pode ser atualizado a qualquer momento, então você deve verificar abaixo quais funções estão implementadas (expandir para mostrar a lista de funções).

<details>
  <summary>Addons</summary>

  - UpdateClientAddon: updateClientAddon(parameters, [callback])
</details>

<details>
  <summary>Affiliates</summary>
  
  - AffiliateActivate: affiliateActivate(parameters, [callback])
  - GetAffiliates: getAffiliates(parameters, [callback])
</details>

<details>
  <summary>Authentication</summary>
  
  - CreateOAuthCredential: createOAuthCredential(parameters, [callback])
  - CreateSsoToken: createSsoToken(parameters, [callback])
  - DeleteOAuthCredential: deleteOAuthCredential(parameters, [callback])
  - ListOAuthCredentials: listOAuthCredentials(parameters, [callback])
  - UpdateOAuthCredential: updateOAuthCredential(parameters, [callback])
  - ValidateLogin: validateLogin(parameters, [callback])
</details>

<details>
  <summary>Billing</summary>

  - AcceptQuote: acceptQuote(parameters, [callback])
  - AddBillableItem: addBillableItem(parameters, [callback])
  - AddCredit: addCredit(parameters, [callback])
  - AddInvoicePayment: addInvoicePayment(parameters, [callback])
  - AddPayMethod: addPayMethod(parameters, [callback])
  - AddTransaction: addTransaction(parameters, [callback])
  - ApplyCredit: applyCredit(parameters, [callback])
  - CapturePayment: capturePayment(parameters, [callback])
  - CreateInvoice: createInvoice(parameters, [callback])
  - CreateQuote: createQuote(parameters, [callback])
  - DeletePayMethod: deletePayMethod(parameters, [callback])
  - DeleteQuote: deleteQuote(parameters, [callback])
  - GenInvoices: genInvoices(parameters, [callback])
  - GetCredits: getCredits(parameters, [callback])
  - GetInvoice: getInvoice(parameters, [callback])
  - GetInvoices: getInvoices(parameters, [callback])
  - GetPayMethods: getPayMethods(parameters, [callback])
  - GetQuotes: getQuotes(parameters, [callback])
  - GetTransactions: getTransactions(parameters, [callback])
  - SendQuote: sendQuote(parameters, [callback])
  - UpdateInvoice: updateInvoice(parameters, [callback])
  - UpdatePayMethod: updatePayMethod(parameters, [callback])
  - UpdateQuote: updateQuote(parameters, [callback])
  - UpdateTransaction: updateTransaction(parameters, [callback])
</details>

<details>
  <summary>Client</summary>

  - AddClient: addClient(parameters, [callback])
  - AddContact: addContact(parameters, [callback])
  - CloseClient: closeClient(parameters, [callback])
  - DeleteClient: deleteClient(parameters, [callback])
  - DeleteContact: deleteContact(parameters, [callback])
  - GetCancelledPackages: getCancelledPackages(parameters, [callback])
  - GetClientGroups: getClientGroups([callback])
  - GetClientPassword: getClientPassword(parameters, [callback])
  - GetClients: getClients(parameters, [callback])
  - GetClientsAddons: getClientsAddons(parameters, [callback])
  - GetClientsDetails: getClientsDetails(parameters, [callback])
  - GetClientsDomains: getClientsDomains(parameters, [callback])
  - GetClientsProducts: getClientsProducts(parameters, [callback])
  - GetContacts: getContacts(parameters, [callback])
  - GetEmails: getEmails(parameters, [callback])
  - UpdateClient: updateClient(parameters, [callback])
  - UpdateContact: updateContact(parameters, [callback])
</details>

<details>
  <summary>Domains</summary>

  - CreateOrUpdateTLD: createOrUpdateTLD(parameters, [callback])
  - DomainGetLockingStatus: domainGetLockingStatus(parameters, [callback])
  - DomainGetNameservers: domainGetNameservers(parameters, [callback])
  - DomainGetWhoisInfo: domainGetWhoisInfo(parameters, [callback])
  - DomainRegister: domainRegister(parameters, [callback])
  - DomainRelease: domainRelease(parameters, [callback])
  - DomainRenew: domainRenew(parameters, [callback])
  - DomainRequestEPP: domainRequestEPP(parameters, [callback])
  - DomainToggleIdProtect: domainToggleIdProtect(parameters, [callback])
  - DomainTransfer: domainTransfer(parameters, [callback])
  - DomainUpdateLockingStatus: domainUpdateLockingStatus(parameters, [callback])
  - DomainUpdateNameservers: domainUpdateNameservers(parameters, [callback])
  - DomainUpdateWhoisInfo: domainUpdateWhoisInfo(parameters, [callback])
  - DomainWhois: domainWhois(parameters, [callback])
  - GetTLDPricing: getTLDPricing(parameters, [callback])
  - UpdateClientDomain: updateClientDomain(parameters, [callback]) 
</details>

<details>
  <summary>Module</summary>

  - ActivateModule: activateModule(parameters, [callback])
  - DeactivateModule: deactivateModule(parameters, [callback])
  - GetModuleConfigurationParameters: getModuleConfigurationParameters(parameters, [callback])
  - GetModuleQueue: getModuleQueue(parameters, [callback])
  - UpdateModuleConfiguration: updateModuleConfiguration(parameters, [callback])
</details>

<details>
  <summary>Module</summary>

  - AcceptOrder: acceptOrder(parameters, [callback])
  - AddOrder: addOrder(parameters, [callback])
  - CancelOrder: cancelOrder(parameters, [callback])
  - DeleteOrder: deleteOrder(parameters, [callback])
  - FraudOrder: fraudOrder(parameters, [callback])
  - GetOrders: getOrders(parameters, [callback])
  - GetOrderStatuses: getOrderStatuses([callback])
  - GetProducts: getProducts(parameters, [callback])
  - GetPromotions: getPromotions(parameters, [callback])
  - OrderFraudCheck: orderFraudCheck(parameters, [callback])
  - PendingOrder: pendingOrder(parameters, [callback])
</details>

<details>
  <summary>Products</summary>

  - AddProduct: addProduct(parameters, [callback])
</details>

<details>
  <summary>Project Management</summary>

  - AddProjectMessage: addProjectMessage(parameters, [callback])
  - AddProjectTask: addProjectTask(parameters, [callback])
  - CreateProject: createProject(parameters, [callback])
  - DeleteProjectTask: deleteProjectTask(parameters, [callback])
  - EndTaskTimer: endTaskTimer(parameters, [callback])
  - GetProject: getProject(parameters, [callback])
  - GetProjects: getProjects(parameters, [callback])
  - StartTaskTimer: startTaskTimer(parameters, [callback])
  - UpdateProject: updateProject(parameters, [callback])
  - UpdateProjectTask: updateProjectTask(parameters, [callback])
</details>

<details>
  <summary>Servers</summary>

  - GetHealthStatus: getHealthStatus(parameters, [callback])
  - GetServers: getServers(parameters, [callback])
</details>


<details>
  <summary>Service</summary>

  - ModuleChangePackage: moduleChangePackage(parameters, [callback])
  - ModuleChangePw: moduleChangePw(parameters, [callback])
  - ModuleCreate: moduleCreate(parameters, [callback])
  - ModuleCustom: moduleCustom(parameters, [callback])
  - ModuleSuspend: moduleSuspend(parameters, [callback])
  - ModuleTerminate: moduleTerminate(parameters, [callback])
  - ModuleUnsuspend: moduleUnsuspend(parameters, [callback])
  - UpdateClientProduct: updateClientProduct(parameters, [callback])
  - UpgradeProduct: upgradeProduct(parameters, [callback])
</details>

<details>
  <summary>Support</summary>

  - AddAnnouncement: addAnnouncement(parameters, [callback])
  - AddCancelRequest: addCancelRequest(parameters, [callback])
  - AddClientNote: addClientNote(parameters, [callback])
  - AddTicketNote: addTicketNote(parameters, [callback])
  - AddTicketReply: addTicketReply(parameters, [callback])
  - blockTicketSender: blockTicketSender(parameters, [callback])
  - DeleteAnnouncement: deleteAnnouncement(parameters, [callback])
  - DeleteTicket: deleteTicket(parameters, [callback])
  - DeleteTicketNote: deleteTicketNote(parameters, [callback])
  - DeleteTicketReply: deleteTicketReply(parameters, [callback])
  - GetAnnouncements: getAnnouncements(parameters, [callback])
  - MergeTicket: mergeTicket(parameters, [callback])
  - OpenTicket: openTicket(parameters, [callback])
  - UpdateTicket: updateTicket(parameters, [callback])
  - UpdateTicketReply: updateTicketReply(parameters, [callback])
</details>


<details>
  <summary>System</summary>

  - AddBannedIp: addBannedIp(parameters, [callback])
  - DecryptPassword: decryptPassword(parameters, [callback])
  - EncryptPassword: encryptPassword(parameters, [callback])
  - GetActivityLog: getActivityLog(parameters, [callback])
  - GetAdminDetails: getAdminDetails([callback])
  - GetAdminUsers: getAdminUsers(parameters, [callback])
  - GetAutomationLog: getAutomationLog(parameters, [callback])
  - GetConfigurationValue: getConfigurationValue(parameters, [callback])
  - GetCurrencies: getCurrencies([callback])
  - GetEmailTemplates: getEmailTemplates(parameters, [callback])
  - GetPaymentMethods: getPaymentMethods([callback])
  - GetStaffOnline: getStaffOnline([callback])
  - GetStats: getStats(parameters, [callback])
  - GetToDoItems: getToDoItems(parameters, [callback])
  - GetToDoItemStatuses: getToDoItemStatuses([callback])
  - LogActivity: logActivity(parameters, [callback])
  - SendAdminEmail: sendAdminEmail(parameters, [callback])
  - SendEmail: sendEmail(parameters, [callback])
  - SetConfigurationValue: setConfigurationValue(parameters, [callback])
  - TriggerNotificationEvent: triggerNotificationEvent(parameters, [callback])
  - UpdateAdminNotes: updateAdminNotes(parameters, [callback])
  - UpdateAnnouncement: updateAnnouncement(parameters, [callback])
  - UpdateToDoItem: updateToDoItem(parameters, [callback])
  - WhmcsDetails: whmcsDetails([callback])
</details>

<details>
  <summary>Tickets</summary>

  - GetSupportDepartments: getSupportDepartments(parameters, [callback])
  - GetSupportStatuses: getSupportStatuses(parameters, [callback])
  - GetTicket: getTicket(parameters, [callback])
  - GetTicketAttachment: getTicketAttachment(parameters, [callback])
  - GetTicketCounts: getTicketCounts(parameters, [callback])
  - GetTicketNotes: getTicketNotes(parameters, [callback])
  - GetTicketPredefinedCats: getTicketPredefinedCats([callback])
  - GetTicketPredefinedReplies: getTicketPredefinedReplies(parameters, [callback])
  - GetTickets: getTickets(parameters, [callback])
</details>

<details>
  <summary>Users</summary>

  - AddUser: addUser(parameters, [callback])
  - CreateClientInvite: createClientInvite(parameters, [callback])
  - DeleteUserClient: deleteUserClient(parameters, [callback])
  - GetPermissionsList: getPermissionsList([callback])
  - GetUserPermissions: getUserPermissions(parameters, [callback])
  - GetUsers: getUsers(parameters, [callback])
  - ResetPassword: resetPassword(parameters, [callback])
  - UpdateUser: updateUser(parameters, [callback])
  - UpdateUserPermissions: updateUserPermissions(parameters, [callback])
</details>


## Testes

Testes foram implementados usando `mocha` e `chai`. Execute-os com `npm test`.
