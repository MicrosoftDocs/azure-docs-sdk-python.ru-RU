---
title: Библиотеки Azure Active Directory для Python
description: Справочная документация по клиентским библиотекам Azure Active Directory для Python
keywords: Azure, Python, SDK, API, SQL, authentication, AAD, Active Directory, Graph, OAuth 2.0
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 08/07/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: active-directory
ms.openlocfilehash: 78df70001dd0d55ac2c9c9da04fac6a51c5919e6
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/23/2018
ms.locfileid: "29478927"
---
# <a name="azure-active-directory-libraries-for-python"></a>Библиотеки Azure Active Directory для Python

## <a name="overview"></a>Обзор

Для входа пользователей в приложения и управления доступом к приложениям и API-интерфейсам можно использовать [Azure Active Directory](/azure/active-directory/active-directory-whatis).

## <a name="client-library"></a>Клиентская библиотека

Настройте проверку подлинности с помощью OAuth2, OpenID Connect или Active Directory Graph и единый вход через [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) с помощью библиотеки [Azure Active Directory Authentication Library (ADAL) для Python](https://github.com/AzureAD/azure-activedirectory-library-for-python).

```bash
pip install azure-graphrbac
```

### <a name="example"></a>Пример
> [!NOTE]
> При создании экземпляра учетных данных необходимо изменить значение параметра resource на https://graph.windows.net.

```python
from azure.graphrbac import GraphRbacManagementClient
from azure.common.credentials import UserPassCredentials

credentials = UserPassCredentials(
            'user@domain.com',      # Your user
            'my_password',          # Your password
            resource="https://graph.windows.net"
    )

tenant_id = "myad.onmicrosoft.com"

graphrbac_client = GraphRbacManagementClient(
    credentials,
    tenant_id
)
```
Следующий код создает пользователя, получает его данные напрямую и с помощью фильтрации списка, а затем удаляет его.
```python
from azure.graphrbac.models import UserCreateParameters, PasswordProfile

user = graphrbac_client.users.create(
    UserCreateParameters(
        user_principal_name="testbuddy@{}".format(MY_AD_DOMAIN),
        account_enabled=False,
        display_name='Test Buddy',
        mail_nickname='testbuddy',
        password_profile=PasswordProfile(
            password='MyStr0ngP4ssword',
            force_change_password_next_login=True
        )
    )
)
# user is a User instance
self.assertEqual(user.display_name, 'Test Buddy')

user = graphrbac_client.users.get(user.object_id)
self.assertEqual(user.display_name, 'Test Buddy')

for user in graphrbac_client.users.list(filter="displayName eq 'Test Buddy'"):
    self.assertEqual(user.display_name, 'Test Buddy')

graphrbac_client.users.delete(user.object_id)
```

> [!div class="nextstepaction"]
> [Обзор клиентских API-интерфейсов](/python/api/overview/azure/activedirectory/client)

Ознакомьтесь с другими [примерами кода Python для Azure AD](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=python), которые можно использовать в приложениях.