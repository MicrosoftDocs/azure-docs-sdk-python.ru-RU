---
title: Библиотеки RBAC Graph для Python
description: Справочник по библиотекам RBAC Graph для Python
keywords: Azure, python, SDK, API, Graph RBAC
author: rloutlaw
ms.author: routlaw
manager: jfriend
ms.date: 05/10/2019
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: e9b0aba7998565284ae18e0036da96d033b2b05f
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534279"
---
# <a name="azure-active-directory-graph-libraries-for-python"></a>Библиотеки Azure Active Directory Graph для Python

> [!IMPORTANT]
>
> С февраля 2019 г. мы начали процесс по прекращению поддержки некоторых ранних версий API Graph для Azure Active Directory с переходом на API Microsoft Graph. 
>
> Подробные сведения, новости и сроки см. в записи блога [Microsoft Graph or the Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) (Microsoft Graph или Azure AD Graph) в Центре разработчиков Office.
>
> Со временем программы должны использовать API Graph Microsoft. 

## <a name="overview"></a>Обзор 

Для входа пользователей и управления доступом к приложениям и интерфейсам API можно использовать [Active Directory Graph](/azure/active-directory/develop/active-directory-graph-api).    

## <a name="client-library"></a>Клиентская библиотека   

 ```bash    
pip install azure-graphrbac 
``` 

### <a name="example"></a>Пример 
> [!NOTE]   
> Вам необходимо изменить параметр ресурса на https://graph.windows.net при создании экземпляра учетных данных.    
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