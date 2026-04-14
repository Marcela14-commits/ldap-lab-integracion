# 📄 ldap_configuracion.md

## 🔹 1. ¿Qué es LDAP?

LDAP (Lightweight Directory Access Protocol) es un protocolo que permite gestionar información de usuarios, grupos y recursos de forma centralizada. Se utiliza comúnmente en organizaciones para administrar accesos, autenticación y estructura organizacional.

Permite almacenar datos como:

* Usuarios
* Contraseñas
* Grupos
* Unidades organizativas (OU)

---

## 🔹 2. Arquitectura creada

Se configuró un servidor LDAP con el dominio:

```
dc=fitpower,dc=local
```

Estructura general:

```
dc=fitpower,dc=local
 └── ou=Finanzas
      ├── uid=fin1
      └── cn=finanzas
```

---

## 🔹 3. Comandos utilizados

### 🔸 Crear OU Finanzas

```bash
ldapadd -x -D cn=admin,dc=fitpower,dc=local -W -f finanzas.ldif
```

### 🔸 Crear grupo Finanzas

```bash
ldapadd -x -D cn=admin,dc=fitpower,dc=local -W -f grupo_finanzas.ldif
```

### 🔸 Crear usuario fin1

```bash
ldapadd -x -D cn=admin,dc=fitpower,dc=local -W -f usuario_fin1.ldif
```

### 🔸 Validar estructura LDAP

```bash
ldapsearch -x -b dc=fitpower,dc=local
```

---

## 🔹 4. Estructura creada

### 📁 Unidad Organizativa

* **Finanzas**

### 👤 Usuario

* **fin1**

  * UID: 1003
  * Grupo: finanzas
  * Home: /home/fin1

### 👥 Grupo

* **finanzas**

  * GID: 5002

---

## 🔹 5. Archivos LDIF utilizados

### 📄 finanzas.ldif

```ldif
dn: ou=Finanzas,dc=fitpower,dc=local
objectClass: organizationalUnit
ou: Finanzas
```

### 📄 grupo_finanzas.ldif

```ldif
dn: cn=finanzas,ou=Finanzas,dc=fitpower,dc=local
objectClass: posixGroup
cn: finanzas
gidNumber: 5002
```

### 📄 usuario_fin1.ldif

```ldif
dn: uid=fin1,ou=Finanzas,dc=fitpower,dc=local
objectClass: top
objectClass: person
objectClass: organizationalPerson
objectClass: inetOrgPerson
objectClass: posixAccount
objectClass: shadowAccount
uid: fin1
cn: Fin One
sn: One
uidNumber: 1003
gidNumber: 5002
homeDirectory: /home/fin1
loginShell: /bin/bash
userPassword: 1234
```

---

## 🔹 6. Evidencias

📸 A continuación se incluyen capturas de:

* Creación de OU Finanzas
* Creación de grupo finanzas
* Creación de usuario fin1
* Resultado del comando `ldapsearch`

![Creación OU](Finanzas.png)
![Grupo finanzas](Grupo_finanzas.png)
![Usuario fin1](Usuario.png)
![Validación LDAP](Validacion1.png)
![Validación LDAP](Validacion2.png)

---

## ✅ Conclusión

Se logró implementar correctamente un entorno LDAP funcional, permitiendo la creación y gestión de unidades organizativas, usuarios y grupos. Esto evidencia el uso de LDAP como herramienta para la administración centralizada de recursos en una organización.

---
