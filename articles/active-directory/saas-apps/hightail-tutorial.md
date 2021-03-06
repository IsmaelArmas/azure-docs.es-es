---
title: 'Tutorial: Integración de Azure Active Directory con Hightail | Microsoft Docs'
description: Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Hightail.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2018
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: bd49d97431efc3e1902e700a54627d5ee095cc74
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/13/2019
ms.locfileid: "56180035"
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a>Tutorial: Integración de Azure Active Directory con Hightail

En este tutorial, aprenderá a integrar Hightail con Azure Active Directory (Azure AD).

Integrar Hightail con Azure AD le proporciona las siguientes ventajas:

- Puede controlar en Azure AD quién tiene acceso a Hightail.
- Puede permitir que los usuarios inicien sesión automáticamente en Hightail (inicio de sesión único) con sus cuentas de Azure AD.
- Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.

Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Requisitos previos

Para configurar la integración de Azure AD con Hightail, se necesitan los siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Hightail

> [!NOTE]
> Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.

Para probar los pasos de este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. El escenario descrito en este tutorial consta de dos bloques de creación principales:

1. Adición de Hightail desde la galería
1. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-hightail-from-the-gallery"></a>Adición de Hightail desde la galería
Para configurar la integración de Hightail en Azure AD, será preciso que agregue Hightail desde la galería a la lista de aplicaciones SaaS administradas.

**Para agregar Hightail desde la galería, realice los pasos siguientes:**

1. En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**. 

    ![Active Directory][1]

1. Vaya a **Aplicaciones empresariales**. A continuación, vaya a **Todas las aplicaciones**.

    ![APLICACIONES][2]
    
1. Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.

    ![APLICACIONES][3]

1. En el cuadro de búsqueda, escriba **Hightail**.

    ![Creación de un usuario de prueba de Azure AD](./media/hightail-tutorial/tutorial_hightail_search.png)

1. En el panel de resultados, seleccione **Hightail** y haga clic en el botón **Agregar** para agregar la aplicación.

    ![Creación de un usuario de prueba de Azure AD](./media/hightail-tutorial/tutorial_hightail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Hightail con un usuario de prueba llamado "Britta Simon".

Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Hightail para un usuario de Azure AD. Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Hightail.

Para establecer la relación de vínculo, en Hightail, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.

Para configurar y probar el inicio de sesión único de Azure AD con Hightail, es preciso completar los siguientes bloques de creación:

1. **[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.
1. **[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.
1. **[Crear un usuario de prueba de Hightail](#creating-a-hightail-test-user)** : para tener un homólogo de Britta Simon en Hightail que esté vinculado a la representación del usuario en Azure AD.
1. **[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.
1. **[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Hightail.

**Para configurar el inicio de sesión único de Azure AD con Hightail, realice los pasos siguientes:**

1. En Azure Portal, en la página de integración de la aplicación **Hightail**, haga clic en **Inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

1. En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.

    ![Configurar inicio de sesión único](./media/hightail-tutorial/tutorial_hightail_samlbase.png)

1. En la sección **Dominio y direcciones URL de Hightail**, realice los siguientes pasos si desea configurar la aplicación en el modo iniciado por **IDP**:

    ![Configurar inicio de sesión único](./media/hightail-tutorial/tutorial_hightail_url.png)

    En el cuadro de texto **URL de respuesta**, escriba la dirección URL como se muestra a continuación: `https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`

    > [!NOTE]
    > El valor de URL de respuesta no es real. El valor se actualizará con la dirección URL de respuesta real, que se explica más adelante en el tutorial.

1. Active **Mostrar configuración avanzada de URL** y siga estos pasos si desea configurar la aplicación en el modo iniciado por **SP**:

    ![Configurar inicio de sesión único](./media/hightail-tutorial/tutorial_hightail_url1.png)

    En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL similar a la siguiente: `https://www.hightail.com/loginSSO`

1. En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.

    ![Configurar inicio de sesión único](./media/hightail-tutorial/tutorial_hightail_certificate.png) 

1. La aplicación Hightail espera las aserciones de SAML en un formato concreto. Configure las siguientes notificaciones para esta aplicación. Puede administrar el valor de estos atributos desde la pestaña "**Atributo**" de la aplicación. La siguiente captura de pantalla le muestra un ejemplo de esto. 

    ![Configurar inicio de sesión único](./media/hightail-tutorial/tutorial_hightail_attribute.png) 

1. En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, configure el atributo token de SAML como muestra la imagen y siga estos pasos:
    
    | Nombre del atributo | Valor de atributo |
    | ------------------- | -------------------- |
    | Nombre | user.givenname |
    | Apellidos | user.surname |
    | Email | user.mail |    
    | UserIdentity | user.mail |
    
     a. Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.

    ![Configurar inicio de sesión único](./media/hightail-tutorial/tutorial_officespace_04.png)

    ![Configurar inicio de sesión único](./media/hightail-tutorial/tutorial_officespace_05.png)

    b. En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.

    c. En la lista **Valor**, seleccione el atributo que se muestra para esa fila.

    d. Deje **Espacio de nombres** en blanco.

    e. Haga clic en **Aceptar**.

1. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/hightail-tutorial/tutorial_general_400.png)

1. En la sección **Configuración de Hightail**, haga clic en **Configurar Hightail** para abrir la ventana **Configurar inicio de sesión**. Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.

    ![Configurar inicio de sesión único](./media/hightail-tutorial/tutorial_hightail_configure.png)

    >[!NOTE]
    >Antes de configurar el inicio de sesión único en la aplicación Hightail, incluya su dominio de correo electrónico en la lista de permitidos con el equipo Hightail para que todos aquellos que utilicen este dominio puedan emplear la funcionalidad de inicio de sesión único.

1. En otra ventana del explorador, abra el portal de administración de **Hightail**.

1. Haga clic en el **icono de usuario** de la esquina superior derecha de la página. 

    ![Configurar inicio de sesión único](./media/hightail-tutorial/configure1.png)

1. Haga clic en la pestaña **Ver consola de administración**.

    ![Configurar inicio de sesión único](./media/hightail-tutorial/configure2.png)

1. En el menú de la parte superior, haga clic en la pestaña **SAML** y realice los pasos siguientes:

    ![Configurar inicio de sesión único](./media/hightail-tutorial/configure3.png)

     a. En el cuadro de texto **Login URL** (Dirección URL de inicio de sesión), pegue el valor de **SAML Single Sign-On Service URL** (Dirección URL de inicio de sesión único de SAML) que copió de Azure Portal.

    b. Abra el certificado codificado en Base 64 descargado de Azure Portal en el Bloc de notas, copie su contenido en el Portapapeles y luego péguelo en el cuadro de texto **Certificado SAML**.

    c. Haga clic en **COPIAR** para copiar la dirección URL del consumidor de SAML de la instancia y péguela en el cuadro de texto **URL de respuesta** de la sección **Dominio y direcciones URL** de Hightail de Azure Portal.

    d. Haga clic en **Guardar configuraciones**.

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".

![Creación de un usuario de Azure AD][100]

**Siga estos pasos para crear un usuario de prueba en Azure AD:**

1. En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.

    ![Creación de un usuario de prueba de Azure AD](./media/hightail-tutorial/create_aaduser_01.png) 

1. Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/hightail-tutorial/create_aaduser_02.png) 

1. Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/hightail-tutorial/create_aaduser_03.png) 

1. En la página de diálogo **Usuario**, realice los siguientes pasos:
 
    ![Creación de un usuario de prueba de Azure AD](./media/hightail-tutorial/create_aaduser_04.png) 

     a. En el cuadro de texto **Nombre**, escriba **BrittaSimon**.

    b. En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.

    c. Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.

    d. Haga clic en **Create**(Crear).
 
### <a name="creating-a-hightail-test-user"></a>Crear un usuario de prueba de Hightail

El objetivo de esta sección es crear un usuario llamado Britta Simon en Hightail. 

No hay ningún elemento de acción para usted en esta sección. Hightail admite el aprovisionamiento Just-In-Time de usuarios en función de las notificaciones personalizadas. Si ha configurado las notificaciones personalizadas como se muestra en la anterior sección **[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** , se creará automáticamente un usuario en la aplicación, si es que todavía no existe uno. 

>[!NOTE]
>Si necesita crear un usuario manualmente, debe ponerse en contacto con el [equipo de soporte técnico de Hightail](mailto:support@hightail.com). 

### <a name="assigning-the-azure-ad-test-user"></a>Asignación del usuario de prueba de Azure AD

En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure, para lo que le concederá acceso a Hightail.

![Asignar usuario][200] 

**Para asignar a Britta Simon a Hightail, realice los pasos siguientes:**

1. En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.

    ![Asignar usuario][201] 

1. En la lista de aplicaciones, seleccione **Hightail**.

    ![Configurar inicio de sesión único](./media/hightail-tutorial/tutorial_hightail_app.png) 

1. En el menú de la izquierda, haga clic en **Usuarios y grupos**.

    ![Asignar usuario][202]

1. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

1. En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.

1. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

1. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.

### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.

Al hacer clic en el icono de Hightail en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Hightail.


## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory](tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/hightail-tutorial/tutorial_general_01.png
[2]: ./media/hightail-tutorial/tutorial_general_02.png
[3]: ./media/hightail-tutorial/tutorial_general_03.png
[4]: ./media/hightail-tutorial/tutorial_general_04.png

[100]: ./media/hightail-tutorial/tutorial_general_100.png

[200]: ./media/hightail-tutorial/tutorial_general_200.png
[201]: ./media/hightail-tutorial/tutorial_general_201.png
[202]: ./media/hightail-tutorial/tutorial_general_202.png
[203]: ./media/hightail-tutorial/tutorial_general_203.png

