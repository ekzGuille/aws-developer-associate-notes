# IAM
Identity Access Management

## Introducción
* Control centralizado de las cuentas de AWS
* Identidad Federada (incluye Active Directory, Facebook, Linkedin...)
* Permite Multifactor de autentificación
* Gestiona todo el control de usuarios/dispositivos externos a los propios servicios de AWS

## Componentes

Desde el IAM puedes gestionar:
* **Usuarios**
* **Grupos**: Conjunto de usuarios con unos permisos (_políticas_) comunes
* **Roles**: Conjunto de permisos (_políticas_) que se asignan a servicios (para que estos puedan interactuar con otros)
* **Policies**: Documento que refleja un cojunto de permisos (_políticas_). (Éstas políticas son las que se adjuntan a Usuarios, Grupos y Roles)
  * Tienen el siguiente formato:
    ```json
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Action": "*", // también puede ser un [] con el listado de acciones dentro
          "Resource": "*"
        }
      ]
    }
    ```
    [Más ejemplos](https://docs.aws.amazon.com/es_es/AmazonS3/latest/dev/example-policies-s3.html)

## Lab
* IAM es **global** (aplica a todas las regiones a la vez)
* A una cuenta de AWS se puede acceder con 2 tipos de usuario:
  * Con la cuenta ROOT:
    * Email
    * Contraseña
  * Con un usuario creado: 
    * Email
    * Contraseña
    * **ID** de la cuenta o **alias**

* Este **alias** es único entre todas las cuentas de AWS
* A un usuario se le pueden aplicar políticas (permisos) a través de un grupo y/o de manera directa (política a política)

* Un usuario puede tener 2 tipos de acceso:
  * Acceso a consola
    * Usuario
    * Contraseña
  * Acceso al CLI/APIs
    * Access Key ID
    * Secret Access Key

* Se pueden cear políticas personalizadas de contraseña (requerimientos de ésta: *longitud, carácteres especiales, etc*)

# STS
Security Token Service. **Puede durar entre 1 y 36 horas**.

* Se utiliza para dar acceso temporal a los recursos de AWS
* Los usuarios pueden venir de:
  * Federation (Active Directory)
    * El usuario se logea con el usuario del Directorio Activo. (No necesita estar dado de alta en el IAM) 
  * Federation (con Aplicaciones Móviles)
    * Facebook/ Aamzon/Google...
  * Usuarios de otras cuentas pueden acceder a recursos de cuentas ajenas.


## Términos clave

* **Federation**: Combinar un listado de usuarios de distintos dominios.
  * P.ej: Usuarios de IAM con usuarios de Facebook
* **Identity Broker**: Servicio de unión de identidades (*federar* las identidades)
* **Identity Store**: Servicio como Active Directory, Facebook, Google, etc
* **Identities**: el usuario de un *Identity Store*

## Flujo de Trabajo

1. Se desarrolla un **Identity Broker** que se comunica con el **LDAP** y **AWS STS**.
2. El Identity Broker siempre se comunica con el **LDAP primero** y **después con AWS STS**.
3. La aplicación obtiene un **acceso temporal** a los servicios de AWS.

# Active directory
* Se puede utilizar con **SAML**ç

## El flujo de trabajo sería el siguiente:
1. El usuario entra a la página de ADFS (página interna de la compañía que requiere login)
2. Automáticamente le redirigirá a una página de Single-Sign-On para que se logee con su usuario y contraseña del Directorio Activo.
3. En el navegador (p. ej. *cookies*) se guarda un flag como que éste se ha registrado.
4. El navegador realiza un **POST** al Endpoint de SAML de AWS: http://signin.aws.amazon.com/saml.
    1. En segundo plano, se está utilizando la API `AssumeRoleWithSAML` para obtener crecenciales temporales y crear la URL de sign-in de la consola.
5. El navegador recibe la URL de sign-in y se le redirige a la consola de AWS.

# Federation With Mobile Applications

1. Entras al enlace: https://web-identity-federation-playground.s3.amazonaws.com/index.html
2. Te logeas con uno de los **proveedores externos**: Facebook, Google o Amazon.
3. Obtienes un token y credenciales temporales
4. Asumes el rol `AssumeRoleWithWebIdentity`
5. Ya puedes acceder a tu recurso de AWS

---

[<small>⬅ Atrás</small>](./index.md)