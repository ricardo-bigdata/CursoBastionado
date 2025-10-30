# Inventario de hardware
## Rack interconexión infraestrutura do centro
1xRack Aula de reforzo de Ciberseguridade - R23
- Switch: D-Link DGS-1250-28X/E
- Latiguiños e transceptores 10GBase-LR:
   - 4 x 10G SFP+ LR Singlemode Transceiver, 10GBase-LR LC Module. 
   - 4 latiguitllos fibra =>  LC to LC 0.5m single mode.
- 1 Patch panel con 11 tomas Cat. 6 postos aula
- 1 toma Ethernet cat. 8 conectada a Sala Dámaso
- 2 tomas monomodo conectadas a Sala Dámaso

## Racks Servidores Proxmox CE Ciberseguridade
1xRack Servidores - R2
rack 19" de 22 U para os servidores
medidas 800x1000
3x regleta de 24 enchufes
patch panel 1x24

- Switch:
- 3 x DELL Optiplex
   - RAM:
   - Procesadores:
   - Discos:
      - Sistema operativo: 2x           en RAID 1
      - Sistema distribuído: 
   - Interfaces de rede:

## Rack Comunicacións CE Ciberseguridade
1xRack Redes - R1
rack 19" de 42 U para os switches
medidas 800x600
regleta de 24 enchufes
patch panel 2x24

- Switch:

# Nomenclatura
## Racks - RKxx
RK01 -> Rack de comunicacións (switches)
RK02 -> Rack de servidores e almacenamento (Proxmox)  

## Regletas enchufes / schukos (Power Distribution Unit) - PDUxx
PDU01 -> PDU arriba
PDU02 -> PDU abaixo
PDU03 -> PDU máis abaixo

Tomas individuais - SKxx
SK01 -> Schuko esquerda
SK02 -> Schuko dereita
SK03 -> Schuko máis á dereita


## Switches - SWxx
SW01 -> Switch arriba
SW02 -> Switch abaixo
SW03 -> Switch máis abaixo

## Patch panels - PPxx
PP01 -> Patch Panel arriba
PP02 -> Patch Panel abaixo
PP03 -> Patch Panel máis abaixo

## Tomas Ethernet - TExx
TE01 -> Toma Ethernet - Punto 01
TE02 -> Toma Ethernet - Punto 02

## Tomas fibra - TFxx
TF01 -> Toma Fibra Monomodo - Punto 01
TF02 -> Toma Fibra Monomodo - Punto 02

## Servidores - srvpvexx
srvpve01 -> Servidor arriba
srvpve02 -> Servidor abaixo
srvpve03 -> Servidor máis abaixo

## SAI
UPS01 -> UPS Principal

## Cables - orixe-destino
SW01-TE24 -> SW02-TE01  -> Cable de Switch01 - porto 24 a Switch02 - porto 01

# Rangos de redes 
- Servidores: 192.168.14.0/24
- ILO:
- Máquinas virtuais:

# Credenciais de acceso
BIOS servidores
Servidores
Switches


# Plan de traballo
Descrición do proceso dende o desempaquetado ata ter un clúster Proxmox completamente funcional montado en rack. 
Executar cada fase de forma secuencial e verificar cada paso antes de continuar.

## Fase 1: Planificación e Preparación

### 1.1. Verificación de Hardware
- [ ] Comprobar que os 3 DELL Optiplex son modelos compatibles con Proxmox
- [ ] Comprobar que dispón de 2 discos SSD para o sistema (usaranse en RAID 1)
- [ ] Comprobar que dispón de discos mecánicos para o sistema de arquivos distribuído (NON SE MONTA NINGÚN RAID SOBRE ELES)
- [ ] Verificar que as tarxetas de fibra son compatibles cos Optiplex
- [ ] Confirmar dispoñibilidade de raíles DELL específicos para o modelo Optiplex
- [ ] Preparar cables de fibra óptica LC-LC ou SC-SC segundo as tarxetas
- [ ] Ter a man switches de fibra ou direct-attach cables para interconexión

### 1.2. Recursos Necessarios
- [ ] USB de 8GB+ para instalación de Proxmox
- [ ] ISO de Proxmox VE 8.x última versión
- [ ] Monitor, teclado e rato temporal
- [ ] Ferramentas de montaxe en rack (só un desaparafusador plano? para poder abri-lo chasis dos servidores e instala-las tarxetas de rede -e eventuais discos extra-)
- [ ] Etiquetas para cableado
- [ ] Documentación de rede (IPs, VLANs, etc.)

## Fase 2: Desempaquetado e Configuración Hardware

### 2.1. Desempaquetado e Verificación
```bash
# Para cada servidor:
1. Desempaquetar nunha superficie limpa e antiestática
2. Verificar que non hai danos visibles no transporte
3. Retirar protecións de embalaxe
4. Comprobar accesorios incluídos (cables, documentación)
5. Etiquetar cada servidor (srvpve01, srvpve02, srvpve-03)
```

### 2.2. Instalación de Componentes
```bash
1. Apagar e desenchufar cada servidor
2. Abrir chasis segundo manual DELL
3. Instalar tarxetas de fibra en slots PCIe dispoñibles
4. Verificar que as tarxetas están firmemente asentadas
5. Pechar chasis e asegurar tódolos parafusos
```

### 2.3. Configuración BIOS/UEFI
```bash
# Acceder a BIOS (F2 durante arranque)
1. Configurar modo UEFI (recomendado)
2. Activar Virtualization Technology (VT-x/VT-d)
3. Configurar arranque por orde: USB -> SSD/HDD
4. Establecer data/hora correcta
5. Gardar configuración e saír
```

## Fase 3: Instalación de Proxmox VE

### 3.1. Preparación USB de Instalación
```bash
# En ordenador de traballo:
1. Descargar Proxmox VE ISO desde proxmox.com
2. Usar Rufus para crear USB booteable
3. Verificar que o USB é booteable
```

### 3.2. Instalación do Sistema
```bash
# Para CADA servidor:
1. Conectar USB de instalación
2. Arrancar e premer F11 para Boot Menu
3. Seleccionar USB boot device
4. Seguir instalación gráfica de Proxmox:

   - Aceptar EULA
   - Seleccionar disco de destino (SSD recomendado)
   - Configurar:
     * País: Spain
     * Zona horaria: Europe/Madrid
     * Teclado: es
   - Configurar rede:
     * Hostname: srvpve01, srvpve02, srvpve03
     * IP address: 192.168.14.10/11/12 (según plan)
     * Gateway: 192.168.14.1
     * DNS: 192.168.10.101????
   - Configurar password de root
   - Configurar email de administración
   - Esperar a que complete instalación
   - Retirar USB e reiniciar
```

### 3.3. Configuración Post-Instalación
```bash
# Acceder vía web: https://IP_SERVIDOR:8006

1. Para cada nodo:
   - Login con root e password
   - Actualizar repositorios:
     sed -i 's/^deb/#deb/' /etc/apt/sources.list.d/pve-enterprise.list
     echo "deb http://download.proxmox.com/debian/pve bookworm pve-no-subscription" > /etc/apt/sources.list.d/pve-no-subscription.list
   
   - Actualizar sistema:
     apt update && apt dist-upgrade -y
   
   - Reiniciar para aplicar updates
```

## Fase 4: Configuración iDRAC

### 4.1. Configuración iDRAC Básica
```bash
# Os servidores DELL Optiplex teñen iDRAC:
1. Arrancar e premer F2 durante boot
2. Navegar a iDRAC Settings
3. Configurar:
   - Network: DHCP ou IP estática
   - Usuario: root (ou personalizado)
   - Password seguro
   - Habilitar acceso web
4. Gardar e saír
```

### 4.2. Acceso iDRAC
```bash
# Desde navegador web:
1. Conectar a https://IP_iDRAC
2. Login con credenciais configuradas
3. Verificar:
   - Estado de hardware
   - Temperaturas
   - Logs de sistema
```

## Fase 5: Configuración do Clúster Proxmox

### 5.1. Creación do Clúster
```bash
# En srvpve01 (primeiro nodo):
pvecm create cluster-proxmox

# En srvpve02 e srvpve03:
pvecm add IP_srvpve01
```

### 5.2. Configuración de Rede para Clúster
```bash
# Configurar corosync para tráfico de clúster:
1. En cada nodo, editar /etc/pve/corosync.conf
2. Verificar que todos os nodos están listados
3. Configurar rede dedicada se é posible para tráfico de clúster
```

### 5.3. Configuración de Almacenamento Compartido
```bash
# Segundo a infraestrutura dispoñible:
1. Configurar NFS, Ceph ou outro almacenamento compartido
2. Engadir almacenamento no clúster
3. Verificar acceso desde todos os nodos
```

## Fase 6: Montaxe en Rack

### 6.1. Preparación do Rack
```bash
1. Verificar que o rack está nivelado e seguro
2. Planificar posición de cada servidor (U)
3. Preparar raíles segundo instrucións DELL
4. Verificar que hai espazo para cableado traseiro
```

### 6.2. Instalación dos Raíles
```bash
# Para cada servidor:
1. Instalar pezas laterais nos servidores
2. Montar raíles externos no rack
3. Verificar que os raíles están nivelados
4. Comprobar mecanismo de bloqueo/desbloqueo
```

### 6.3. Montaxe dos Servidores
```bash
1. Con axuda, levantar cada servidor á altura do rack
2. Enganchar parte traseira dos raíles primeiro
3. Empuxar suavemente até que encaixe na parte dianteira
4. Asegurar con parafusos de seguridade se é necesario
5. Verificar que o servidor despraza suavemente
```

### 6.4. Cableado Organizado
```bash
1. Cableado de rede:
   - Conexión management (1Gbps)
   - Conexións de fibra para cluster/comunicación
   - Conexión iDRAC se existe

2. Cableado de potencia:
   - Conectar a PDU do rack
   - Usar diferentes circuitos se é posible
   - Organizar cables con bridas

3. Etiquetar todos os cables:
   - Servidor de destino
   - Tipo de conexión
   - VLAN se aplicable
```

## Fase 7: Verificación Final

### 7.1. Comprobación de Hardware
```bash
1. Encender todos os servidores
2. Verificar que arrancan correctamente
3. Comprobar que as tarxetas de fibra son detectadas
4. Verificar conectividade de rede
```

### 7.2. Comprobación do Clúster
```bash
# Desde pve-01:
pvecm status
pvecm nodes

# Verificar en web interface:
- Todos os nodos aparecen no clúster
- Estado "online" para todos
- Almacenamento compartido accesible
```

### 7.3. Test de Migración
```bash
1. Crear unha VM de proba nun nodo
2. Migrar en vivo a outro nodo
3. Verificar que a migración foi exitosa
4. Comprobar conectividade de rede na VM
```

## Fase 8: Documentación

### 8.1. Crear Documentación do Clúster
```bash
1. Listar IPs de cada servidor e iDRAC
2. Documentar configuración de rede
3. Gardar passwords en xestor seguro
4. Crear diagrama de rede
5. Documentar procedementos de backup
```

## Notas Importantes:

1. **Seguridade**: Cambiar passwords por defecto inmediatamente
2. **Backup**: Configurar backup da configuración de Proxmox
3. **Monitorización**: Configurar alertas por email
4. **Mantemento**: Planificar períodos de actualización

