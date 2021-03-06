---
title: 'Tutorial: Integración de Azure Active Directory con Flatter Files | Microsoft Docs'
description: Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Flatter Files.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: f86fe5e3-0e91-40d6-869c-3df6912d27ea
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 744d18b39ffc696d0973628c60687c6b70fbcaad
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/13/2019
ms.locfileid: "56168687"
---
# <a name="tutorial-azure-active-directory-integration-with-flatter-files"></a>Tutorial: Integración de Azure Active Directory con Flatter Files

En este tutorial, aprenderá a integrar Flatter Files con Azure Active Directory (Azure AD).

Integrar Flatter Files con Azure AD le proporciona las siguientes ventajas:

- Puede controlar en Azure AD quién tiene acceso a Flatter Files.
- Puede permitir que los usuarios inicien sesión automáticamente en Flatter Files (inicio de sesión único) con sus cuentas de Azure AD.
- Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.

Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Requisitos previos

Para configurar la integración de Azure AD con Flatter Files, necesita los siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Flatter Files

> [!NOTE]
> Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.

Para probar los pasos de este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. El escenario descrito en este tutorial consta de dos bloques de creación principales:

1. Adición de Flatter Files desde la galería
1. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-flatter-files-from-the-gallery"></a>Adición de Flatter Files desde la galería
Para configurar la integración de Flatter Files en Azure AD, deberá agregar Flatter Files desde la galería a la lista de aplicaciones SaaS administradas.

**Para agregar Flatter Files desde la galería, realice los pasos siguientes:**

1. En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**. 

    ![Active Directory][1]

1. Vaya a **Aplicaciones empresariales**. A continuación, vaya a **Todas las aplicaciones**.

    ![APLICACIONES][2]
    
1. Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.

    ![APLICACIONES][3]

1. En el cuadro de búsqueda, escriba **Flatter Files**.

    ![Creación de un usuario de prueba de Azure AD](./media/flatter-files-tutorial/tutorial_flatterfiles_search.png)

1. En el panel de resultados, seleccione **Flatter Files** y luego haga clic en el botón **Agregar** para agregar la aplicación.

    ![Creación de un usuario de prueba de Azure AD](./media/flatter-files-tutorial/tutorial_flatterfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con Flatter Files con un usuario de prueba llamado "Britta Simon".

Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Flatter Files para un usuario de Azure AD. Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Flatter Files.

Para establecer la relación de vínculo, en Flatter Files, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.

Para configurar y probar el inicio de sesión único de Azure AD con Flatter Files, es preciso completar los siguientes bloques de creación:

1. **[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.
1. **[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.
1. **[Creación de un usuario de prueba de Flatter Files](#creating-a-flatter-files-test-user)**: para tener un homólogo de Britta Simon en CS Stars que esté vinculado a la representación del usuario en Azure AD.
1. **[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.
1. **[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Flatter Files.

**Para configurar el inicio de sesión único de Azure AD con Flatter Files, realice los pasos siguientes:**

1. En Azure Portal, en la página de integración de la aplicación **Flatter Files**, haga clic en **Inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

1. En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/flatter-files-tutorial/tutorial_flatterfiles_samlbase.png)

1. En la sección **Dominio y direcciones URL de Flatter Files**, el usuario no tiene que realizar ningún paso ya que la aplicación se ha integrado previamente con Azure.

    ![Configurar inicio de sesión único](./media/flatter-files-tutorial/tutorial_flatterfiles_url.png)
 
1. En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.

    ![Configurar inicio de sesión único](./media/flatter-files-tutorial/tutorial_flatterfiles_certificate.png) 

1. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/flatter-files-tutorial/tutorial_general_400.png)

1. En la sección **Configuración de Flatter Files**, haga clic en **Configurar Flatter Files** para abrir la ventana **Configurar inicio de sesión**. Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.

    ![Configurar inicio de sesión único](./media/flatter-files-tutorial/tutorial_flatterfiles_configure.png) 

1. Inicie sesión en su aplicación de Flatter Files como administrador.

1. Haga clic en **PANEL**. 
   
    ![Configurar inicio de sesión único](./media/flatter-files-tutorial/tutorial_flatter_files_05.png)  

1. Haga clic en **Settings** (Configuración) y, después, siga estos pasos siguientes en la pestaña **Company** (Compañía): 
   
    ![Configurar inicio de sesión único](./media/flatter-files-tutorial/tutorial_flatter_files_06.png)  
    
     a. Seleccione **Usar SAML 2.0 para autenticación**.
    
    b. Haga clic en **Configurar SAML**.

1. En el cuadro de diálogo **Configuración de SAML** , realice los siguientes pasos: 
   
    ![Configurar inicio de sesión único](./media/flatter-files-tutorial/tutorial_flatter_files_08.png)  
   
     a. En el cuadro de texto **Dominio**, escriba el dominio registrado.
   
    >[!NOTE]
    >Si no dispone de un dominio registrado, póngase en contacto con el equipo de soporte técnico de Flatter Files a través de [support@flatterfiles.com](mailto:support@flatterfiles.com). 
    
    b. En el cuadro de texto **Identity Provider URL** (Dirección URL del proveedor de identidades), pegue el valor de **Dirección URL del servicio de inicio de sesión único de SAML** que ha copiado en Azure Portal.
   
    c.  Abra el certificado codificado en base 64 en el Bloc de notas, copie su contenido en el Portapapeles y luego péguelo en el cuadro de texto **Certificado de proveedor de identidades**.

    d. Haga clic en **Update**(Actualizar).

> [!TIP]
> Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.  Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior. Puede leer más aquí sobre la característica de documentación insertada: [Documentación insertada de Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".

![Creación de un usuario de Azure AD][100]

**Siga estos pasos para crear un usuario de prueba en Azure AD:**

1. En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.

    ![Creación de un usuario de prueba de Azure AD](./media/flatter-files-tutorial/create_aaduser_01.png) 

1. Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/flatter-files-tutorial/create_aaduser_02.png) 

1. Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/flatter-files-tutorial/create_aaduser_03.png) 

1. En la página de diálogo **Usuario**, realice los siguientes pasos:
 
    ![Creación de un usuario de prueba de Azure AD](./media/flatter-files-tutorial/create_aaduser_04.png) 

     a. En el cuadro de texto **Nombre**, escriba **BrittaSimon**.

    b. En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.

    c. Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.

    d. Haga clic en **Create**(Crear).
 
### <a name="creating-a-flatter-files-test-user"></a>Creación de un usuario de prueba de Flatter Files

El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en Flatter Files.

**Para crear una usuaria llamada Britta Simon en Flatter Files, realice los pasos siguientes:**

1. Inicie sesión en su sitio de la compañía de **Flatter Files** como administrador.

1. En el panel de navegación de la izquierda, haga clic en **Configuración** y, luego, en la pestaña **Usuarios**.
   
    ![Creación de un usuario de Flatter Files](./media/flatter-files-tutorial/tutorial_flatter_files_09.png)

1. Haga clic en **Agregar usuario**. 

1. En el cuadro de diálogo **Agregar usuario** , realice los pasos siguientes:
   
    ![Creación de un usuario de Flatter Files](./media/flatter-files-tutorial/tutorial_flatter_files_10.png)

     a. En el cuadro de texto **Nombre**, escriba **Britta**.
   
    b. En el cuadro de texto **Apellidos**, escriba **Simon**. 
   
    c. En el cuadro de texto **Dirección de correo electrónico**, escriba la dirección de correo electrónico de Britta en Azure Portal.
   
    d. Haga clic en **Enviar**.   


### <a name="assigning-the-azure-ad-test-user"></a>Asignación del usuario de prueba de Azure AD

En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Flatter Files.

![Asignar usuario][200] 

**Para asignar a Britta Simon a Flatter Files, realice los pasos siguientes:**

1. En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.

    ![Asignar usuario][201] 

1. En la lista de aplicaciones, seleccione **Flatter Files**.

    ![Configurar inicio de sesión único](./media/flatter-files-tutorial/tutorial_flatterfiles_app.png) 

1. En el menú de la izquierda, haga clic en **Usuarios y grupos**.

    ![Asignar usuario][202] 

1. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

1. En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.

1. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

1. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.

Al hacer clic en el icono de Flatter Files en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Flatter Files.
Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](../user-help/active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory](tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/flatter-files-tutorial/tutorial_general_01.png
[2]: ./media/flatter-files-tutorial/tutorial_general_02.png
[3]: ./media/flatter-files-tutorial/tutorial_general_03.png
[4]: ./media/flatter-files-tutorial/tutorial_general_04.png

[100]: ./media/flatter-files-tutorial/tutorial_general_100.png

[200]: ./media/flatter-files-tutorial/tutorial_general_200.png
[201]: ./media/flatter-files-tutorial/tutorial_general_201.png
[202]: ./media/flatter-files-tutorial/tutorial_general_202.png
[203]: ./media/flatter-files-tutorial/tutorial_general_203.png

