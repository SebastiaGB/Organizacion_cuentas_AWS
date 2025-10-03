# Organización de cuentas en AWS siguiendo buenas prácticas

Este proyecto describe cómo organizar y gestionar varias cuentas de AWS aplicando buenas prácticas de seguridad, centralización y control de accesos.

## 1. Creación de la Organización

Se habilita AWS Organizations en una cuenta de administración central IAM.
Esta cuenta será la encargada de invitar, crear y gestionar el resto de cuentas de la organización.

## 2. Integración de la cuenta de Producción (Cuenta 2)

Se invita a la cuenta de Producción existente a unirse a la organización.
Se crea un rol de acceso en Producción, el cual puede ser asumido desde la Cuenta General.
Así, la Cuenta General puede gestionar Producción de forma centralizada y segura, usando su Account ID, sin necesidad de configurar accesos manuales dentro de Producción.

> Para evitar crear nuevas direcciones de correo, se utiliza el formato de Gmail usuario+nombre@gmail.com.
> Esto permite registrar múltiples cuentas de AWS bajo la misma dirección base, simplificando la administración.

## 4. Creación de la cuenta de Desarrollo (Cuenta 3)

Se crea una nueva cuenta de Desarrollo directamente desde AWS Organizations.
Tras la verificación, se asigna un rol que permite a la Cuenta General acceder y gestionarla de forma centralizada.

## 5. Configuración de IAM Identity Center 

Se habilita IAM Identity Center para gestionar el acceso de los usuarios a todas las cuentas de la organización.
Se genera una URL de inicio de sesión personalizada para que los usuarios accedan a la consola de AWS con permisos temporales y limitados.
Esto elimina la necesidad de credenciales permanentes, reduciendo riesgos de seguridad.

## 6. Definición de conjuntos de permisos

Se crean Permission Sets (conjuntos de permisos) según los perfiles de usuario, por ejemplo:
Billing PowerUsers: acceso a la facturación y a recursos de infraestructura (IaaS).
Otros roles adaptados a los equipos (Desarrollo, Operaciones, Seguridad, etc.).

## 7. Creación de un usuario de prueba

Se crea el usuario 'Alice' en IAM Identity Center.
Alice se asigna a un grupo, y a ese grupo se le otorga un Permission Set, como Billing.
De esta forma, Alice puede acceder a la consola con permisos temporales únicamente sobre los recursos autorizados.
