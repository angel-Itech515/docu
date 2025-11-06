# **Puertos más comunes en Modbus**

1. **502 (Modbus TCP - Oficial)**
    
    - Es el puerto estándar definido por **Modbus Organization** para comunicaciones TCP/IP.
        
    - La mayoría de los PLCs, gateways y dispositivos IoT lo usan por defecto.
        
2. **503, 504, 505 (Modbus TCP alternativos)**
    
    - Algunas aplicaciones y firewalls restringen el puerto 502, por lo que se configuran estos puertos como alternativa.
        
    - Algunos dispositivos permiten cambiar el puerto en la configuración.
        
3. **2000 (Modbus TCP en sistemas embebidos y gateways)**
    
    - Usado por algunos dispositivos embebidos y conversores serie/Ethernet.
        
    - Alternativa en redes industriales que restringen el 502.
        
4. **1502 (Schneider Electric / Modicon)**
    
    - Algunas implementaciones de **Schneider Electric (Modicon)** usan el 1502 en lugar del 502.

# Configurar registros

``` txt
Configuring the ModbusTags in a PlantValue IOPath/IOPathNet.

With the SHIFT ADDR = 0, you need to configure the IOPath/IOPathNet column with the following format:

Slave_ID,    ModBus_Register_Type,    Start_Address,    Number_Of_Registers

ModBus Register Types:

1 = coil  
2 = input  
3 = input register  
4 = holding register

For instance,   IOPathNet=  1,3,0608,2   means Slave_ID=1, type:input register, Register-Addess=608, 2 registers (read Register-Address 608 and 609 as a input register)

With the SHIFT ADDR = -1 , for instance,   IOPathNet=  1,3,0608,2   means Slave_ID=1, type:input register, Modbus-Addess = 608, 2 registers (read Register-Address 607 and 608 as a input register)
```

> El SHIFT ADDR se define a 0 o -1 dependiendo si queremos desplazar los registros una posición o no.
> 
> Algunas notas sobre el funcionamiento de los registros modbus:
> 	cada registre modbus és 16 bits, 2bytes, 1 HalfWord
> 	els bool s'indiquen com 0000,1 per agafar el HalfWord de 16 bits desde 0000
> 	l'offset **depenent del mapa de senyals** indica cada 8 bits, 1 byte
> 	els Reals i Int com 0001,2 per agafar un Word 32 bits (2 HalfWord i 2 registres modbus)|
# Cliente Modscan32

- Usar el fichero SN.txt para activar la licencia pirata.
- Si tras conectar falla, revisa el campo length, lo más seguro es que supere el numero máximo de direcciones y falle.

## Vista con bits

![[Pasted image 20250403165202.png]]

OUTPUT SIGNALS = true (default) //Permet l'enviament de tags de retorn, property1=W
OUTPUT SIGNALS = false //Para l'enviament de tags de retorn, property1=W. No fa falta reiniciar la IF (en teoria)
