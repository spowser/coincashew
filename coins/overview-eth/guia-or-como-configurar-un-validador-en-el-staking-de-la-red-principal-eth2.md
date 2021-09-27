---
description: >-
  Conviértete en un validador y ayuda a asegurar eth2, una cadena de bloques de
  pruebas. Cualquiera con 32 ETH puede unirse.
---

# Guía \| Cómo configurar un validador en el staking de la red principal ETH2

{% hint style="success" %}
A partir del 5 de diciembre de 2020, esta guía se actualiza para **mainnet.**😁
{% endhint %}

🎊 **Actualización 2020-12**: Estamos en [Gitcoin](https://gitcoin.co/grants/1653/eth2-staking-guides-by-coincashew), donde usted puede contribuir a través de [fondos cuadráticos](https://vitalik.ca/general/2019/12/07/quadratic.html) y hacer un gran impacto. Tu contribución de **1 DAI** equivale a **23 DAI** partida.

Por favor, [échanos un vistazo a](https://gitcoin.co/grants/1653/eth2-staking-guides-by-coincashew). Gracias!🙏

{% embed url="https://gitcoin.co/grants/1653/eth2-staking-guides-by-coincashew" caption="" %}

## 🏁 0. Prerrequisitos

### 💻Habilidades para operar un validador eth2 y nodo baliza

Como validador de eth2, normalmente tendrás las siguientes habilidades:

* conocimiento operativo de cómo configurar, ejecutar y mantener un nodo y validador de baliza eth2 continuamente
* un compromiso a largo plazo para mantener su validador 24/7/365
* habilidades básicas del sistema operativo
* han aprendido lo esencial viendo ['Introducción a la Eth2 & Staking for Beginners' por Superphiz](https://www.youtube.com/watch?v=tpkpW031RCI)
* han pasado o está inscrito activamente en el [curso de estudios de Eth2](https://ethereumstudymaster.com/)
* y han leído la [8 Cosas que cada validador de Eth2 debería saber.](https://medium.com/chainsafe-systems/8-things-every-eth2-validator-should-know-before-staking-94df41701487)

### 🎗 **Requisitos mínimos de configuración**

* **Sistema operativo:** Linux de 64-bit \\(i.e. Servidor LTS o escritorio Ubuntu 20.04\)
* **Procesador:** Dual core CPU, Intel Core i5–760 o AMD FX-8100 o mejor
* **Memory:** 8GB RAM
* **Almacenamiento:** 20GB SSD
* **Internet:** Conexión a Internet de banda ancha con velocidades de al menos 1 Mbps.
* **Poder:** Energía eléctrica fiable.
* **Saldo ETH:** al menos 32 ETH y algunos ETH por comisiones de depósito
* **Cartera**: Metamask instalado

### 🏋 Configuración recomendada de hardware

* **Sistema operativo:** Linux de 64-bit \(i.e. Servidor LTS o escritorio Ubuntu 20.04\)
* **Procesador:** Quad core CPU, Intel Core i7–4770 o AMD FX-8310 o mejor
* **Memoria:** RAM de 16GB o más
* **Almacenamiento:** SSD de 1TB o más
* **Internet:** Conexiones a Internet de banda ancha con velocidades de al menos 10 Mbps sin límite de datos.
* **Poder:** Energía eléctrica fiable con alimentación ininterrumpida \(UPS\)
* **Saldo ETH:** al menos 32 ETH y algunos ETH por comisiones de depósito
* **Cartera**: Metamask instalado

{% hint style="success" %}
✨ **Consejo del validador Pro**: Te recomendamos que comences con una nueva instancia de un sistema operativo, máquina virtual y/o máquina. Evite los dolores de cabeza no reutilizando claves de red de pruebas, billeteras, o bases de datos para su validador.
{% endhint %}

### 🔓 Mejores prácticas recomendadas para validadores eth2

Si necesita ideas o un recordatorio sobre cómo asegurar su validador, consulte

### 🛠 Setup Ubuntu

Si necesita instalar el servidor Ubuntu, refiérase a

{% embed url="https://ubuntu.com/tutorials/install-ubuntu-server\#1-overview" caption="" %}

O Escritorio Ubuntu, [https://www.coincashew.com/coins/overview-xtz/guide-how-to-setup-a-baker/install-ubuntu](https://www.coincashew.com/coins/overview-xtz/guide-how-to-setup-a-baker/install-ubuntu)

### 🎭 Configurar Metamask

Si necesita instalar Metamask, consulte [https://www.coincashew.com/wallets/browser-wallets/metamask-ethereum](https://www.coincashew.com/wallets/browser-wallets/metamask-ethereum)

## 🌱 1. Comprar/intercambiar o consolidar ETH

{% hint style="info" %}
Cada 32 ETH que tengas te permite hacer 1 validador. Puede ejecutar miles de validadores con su nodo faro.
{% endhint %}

Su ETH \(o múltiplos de 32 ETH\) debe consolidarse en una sola dirección accesible con Metamask.

Si necesita comprar/intercambiar o recargar su ETH a un múltiplo de 32, eche un vistazo:

{% embed url="https://www.coincashew.com/coins/overview-eth/guide-how-to-buy-eth" %}

## 👩 2. Regístrate para ser un validador en el Launchpad

1. Instale dependencias, la herramienta de depósito de la fundación ethereum y genere sus dos conjuntos de pares de claves.

{% hint style="info" %}
Cada validador tendrá dos conjuntos de pares de claves. Una **clave de firma** y una **clave de retiro.** Estas claves se derivan de una sola frase mnemónica. [Más información sobre claves.](https://blog.ethereum.org/2020/05/21/keys/)
{% endhint %}

Tienes la opción de descargar la [herramienta de depósito de cimientos ethereum](https://github.com/ethereum/eth2.0-deposit-cli) preconstruida o construirla desde la fuente.

{% tabs %}
{% tab title="Construir a partir del código fuente" %}
Instalar dependencias.

```text
sudo apt update
sudo apt install python3-pip git -y
```

Descargar código fuente e instalar.

```text
cd $HOME
git clone https://github.com/ethereum/eth2.0-deposit-cli.git eth2deposit-cli
cd eth2deposit-cli
sudo ./deposit.sh install
```

Crea una nueva mnemónica.

```text
./deposit.sh new-mnemonic --chain mainnet
```
{% endtab %}

{% tab title="Eth2deposit-cli prediseñado" %}
Descargar eth2deposit-cli.

```bash
cd $HOME
wget https://github.com/ethereum/eth2.0-deposit-cli/releases/download/v1.1.0/eth2deposit-cli-ed5a6d3-linux-amd64.tar.gz
```

Verifique que la suma de verificación SHA256 coincide con la suma de verificación en la página de [lanzamientos](https://github.com/ethereum/eth2.0-deposit-cli/releases/tag/v1.0.0).

```bash
echo "2107f26f954545f423530e3501ae616c222b6bf77774a4f2743effb8fe4bcbe7 *eth2deposit-cli-ed5a6d3-linux-amd64.tar.gz" | shasum -a 256 --check
```

Extraer el archivo.

```text
tar -xvf eth2deposit-cli-ed5a6d3-linux-amd64.tar.gz
mv eth2deposit-cli-ed5a6d3-linux-amd64 eth2deposit-cli
rm eth2deposit-cli-ed5a6d3-linux-amd64.tar.gz
cd eth2deposit-cli
```

Crea una nueva mnemónica.

```text
./deposit new-mnemonic --chain mainnet
```
{% endtab %}

{% tab title="Avanzado: más seguro" %}
{% hint style="warning" %}
🔥**\[ Optional \] Consejo de seguridad Pro**: Ejecute la herramienta **eth2deposit-cli** y genere su **semilla mnemónica** para sus claves de validador en una **máquina desconectada desconectada iniciada desde usb**.
{% endhint %}

Siga este [ethstaker.cc](https://ethstaker.cc/) exclusivo para la baja al hacer una usb arrancable.

#### Parte 1 - Crear una unidad USB de arranque Ubuntu 20.04

{% embed url="https://www.youtube.com/watch?v=DTR3PzRRtYU" %}

#### Parte 2 - Instalar Ubuntu 20.04 desde la unidad USB

{% embed url="https://www.youtube.com/watch?v=C97\_6MrufCE" %}

Usted puede copiar a través de USB key los binarios eth2deposit-cli preconstruidos de una máquina en línea a una máquina sin conexión, desconectada, arrancada de usb. Asegúrese de desconectar el cable ethernet y/o WIFI.
{% endtab %}
{% endtabs %}

2. Siga las instrucciones y elija una contraseña. Escribe tu mnemónico y mantén esto seguro y **sin conexión**.

{% hint style="warning" %}
\*\*\*\*🚧 **Precaución**: Solo deposite los 32 ETH por validador si está seguro de que su nodo ETH1 y el validador ETH2 estarán completamente sincronizados y listos para realizar las tareas de validación. Puede volver más tarde a Launchpad con sus datos de depósito para completar los siguientes pasos.
{% endhint %}

3. Sigue los pasos en [https://launchpad.ethereum.org/](https://launchpad.ethereum.org/) mientras te saltas los pasos que ya has completado. Estudiar el material general de la fase eth2 0. ¡Entender eth2 es la clave del éxito!

4. Volver al sitio web de launchpad, sube tu`deposit_data-#######.json` encontrado en el directorio `validator_keys`.

5. Conéctate al Launchpad con tu cartera Metamask, revisa y acepta los términos.

6. Confirmar la transacción\(s\). Hay una transacción de depósito de 32 ETH para cada validador.

{% hint style="info" %}
Your transaction is sending and depositing your ETH to the [official ETH2 deposit contract address. ](https://blog.ethereum.org/2020/11/04/eth2-quick-update-no-19/)

**Compruebe**, _doble verificación_, _**cheque triple**_ que la dirección oficial del contrato de depósito Eth2 es correcta.[`0x000000219ab540356cB839Cbe05303d7705Fa`](https://etherscan.io/address/0x00000000219ab540356cbb839cbe05303d7705fa)
{% endhint %}

{% hint style="danger" %}
🔥 **Recordatorio de Crypto Crítico:** **Mantén tu mnemónica, mantén tu ETH.**🚀

* Escriba su semilla mnemónica **sin conexión**. _No es correo electrónico. No en la nube._
* Múltiples copias son mejores. _Mejor almacenado en una semilla de_ [_de metal._](https://jlopp.github.io/metal-bitcoin-storage-reviews/)
* Las claves de retiro se generarán a partir de este mnemónico en el futuro.
* Hacer **copias de seguridad fuera de línea**, como una clave USB, de su directorio **`validator_keys`**.
{% endhint %}

## 🛸 3. Install a ETH1 node

{% hint style="info" %}
Ethereum 2.0 requiere una conexión a Ethereum 1.0 para monitorear los depósitos de 32 validadores ETH. Alojamiento de su propio nodo Ethereum 1.0 es la mejor manera de maximizar la descentralización y minimizar la dependencia de terceros como Infura.
{% endhint %}

{% hint style="warning" %}
Los pasos siguientes asumen que ha completado la guía de seguridad de mejores prácticas.

🛑 No ejecute sus procesos como usuario de **ROOT**. 😱
{% endhint %}

Tu elección de cualquiera [**OpenEthereum**](https://www.parity.io/ethereum/)**,** [**Geth**](https://geth.ethereum.org/)**,** [**Besu**](https://besu.hyperledger.org/)**,** [**Nethermind**](https://www.nethermind.io/), [**Infura**](https://infura.io/) **or** [**Chainstack**](https://chainstack.com/)**.**

{% tabs %}
{% tab title="OpenEthereum \(Paridad\)" %}
{% hint style="info" %}
**OpenEthereum** - Es **\*\*goal es ser el cliente más rápido, ligero y seguro de Ethereum usando el** lenguaje de programación de Rust\*\*. OpenEthereum está licenciado bajo GPLv3 y puede ser utilizado para todas sus necesidades de Ethereum.
{% endhint %}

#### ⚙ Instalar dependencias

```text
sudo apt-get update
sudo apt-get install curl jq unzip -y
```

#### 🤖 Install OpenEthereum

Revise la última versión en [https://github.com/openethereum/openethereum/releases](https://github.com/openethereum/openethereum/releases)

Descargar automáticamente la última versión de linux, un-zip, añadir permisos de ejecución y limpieza.

```bash
mkdir $HOME/openethereum
cd $HOME/openethereum
curl -s https://api.github.com/repos/openethereum/openethereum/releases/latest | jq -r ".assets[] | select(.name) | .browser_download_url" | grep linux | xargs wget -q --show-progress
unzip -o openethereum*.zip
chmod +x openethereum
rm openethereum*.zip
```

**Configurar y configurar el sistema**

Ejecute lo siguiente para crear un **archivo de unidad** para definir su configuración `eth1.service`.

Simplemente copia/pega lo siguiente.

```bash
cat > $HOME/eth1.service << EOF 
[Unit]
Description     = openethereum eth1 service
Wants           = network-online.target
After           = network-online.target 

[Service]
User            = $(whoami)
ExecStart       = $(echo $HOME)/openethereum/openethereum --metrics --metrics-port=6060
Restart         = on-failure
RestartSec      = 3

[Install]
WantedBy    = multi-user.target
EOF
```

{% hint style="info" %}
**Nimbus Configuración específica**: Añadir la siguiente bandera a la línea **ExecStart**.

```bash
--ws-origins=all
```
{% endhint %}

Mueva el archivo de unidad a `/etc/systemd/system` y otorgue permisos.

```bash
sudo mv $HOME/eth1.service /etc/systemd/system/eth1.service
```

```bash
sudo chmod 644 /etc/systemd/system/eth1.service
```

Ejecute lo siguiente para habilitar auto-inicio en el momento de arranque.

```text
sudo systemctl daemon-reload
sudo systemctl enable eth1
```

#### ⛓ Iniciar OpenEthereum

```text
sudo systemctl start eth1
```
{% endtab %}

{% tab title="Geth" %}
{% hint style="info" %}
**Geth** - Go Ethereum es una de las tres implementaciones originales \(junto con C++ y Python\) del protocolo Ethereum. Está escrito en **Go**, completamente de código abierto y bajo licencia GNU LGPL v3.
{% endhint %}

Revise las últimas notas de la versión en [https://github.com/ethereum/go-ethereum/releases](https://github.com/ethereum/go-ethereum/releases)

#### 🧬 Instalar desde el repositorio

```text
sudo add-apt-repository -y ppa:ethereum/ethereum
sudo apt-get update -y
sudo apt-get install ethereum -y
```

⚙ **Configurar y configurar el sistema**

Ejecute lo siguiente para crear un **archivo de unidad** para definir su configuración `eth1.service`.

Simplemente copia/pega lo siguiente.

```bash
cat > $HOME/eth1.service << EOF 
[Unit]
Description     = geth eth1 service
Wants           = network-online.target
After           = network-online.target 

[Service]
User            = $(whoami)
ExecStart       = /usr/bin/geth --http --metrics --pprof
Restart         = on-failure
RestartSec      = 3
TimeoutSec      = 300

[Install]
WantedBy    = multi-user.target
EOF
```

{% hint style="info" %}
**Nimbus Configuración específica**: Añadir la siguiente bandera a la línea **ExecStart**.

```bash
--ws
```
{% endhint %}

Mueva el archivo de unidad a `/etc/systemd/system` y otorgue permisos.

```bash
sudo mv $HOME/eth1.service /etc/systemd/system/eth1.service
```

```bash
sudo chmod 644 /etc/systemd/system/eth1.service
```

Ejecute lo siguiente para habilitar auto-inicio en el momento de arranque.

```text
sudo systemctl daemon-reload
sudo systemctl enable eth1
```

#### ⛓ Inicio geth

```text
sudo systemctl start eth1
```
{% endtab %}

{% tab title="Besu" %}
{% hint style="info" %}
**Hyperledger Besu** es un cliente Ethereum de código abierto diseñado para aplicaciones empresariales exigentes que requieren un procesamiento de transacciones seguro y de alto rendimiento en una red privada. Está desarrollado bajo la licencia Apache 2.0 y escrito en **Java**.
{% endhint %}

#### 🧬 Instalar dependencia de java

```text
sudo apt update
sudo apt install openjdk-11-jdk -y
```

#### 🌜 Descargar y descomprimir Besu

Revise la última versión en [https://github.com/hyperledger/besu/releases](https://github.com/hyperledger/besu/releases)

El archivo se puede descargar desde [https://dl.bintray.com/hyperledger-org/besu-repo](https://dl.bintray.com/hyperledger-org/besu-repo)

```text
cd
wget -O besu.tar.gz https://dl.bintray.com/hyperledger-org/besu-repo/besu-20.10.1.tar.gz
tar -xvf besu.tar.gz
rm besu.tar.gz
mv besu* besu
```

⚙ **Configurar y configurar el sistema**

Ejecute lo siguiente para crear un **archivo de unidad** para definir su configuración `eth1.service`.

Simplemente copia/pega lo siguiente.

```bash
cat > $HOME/eth1.service << EOF 
[Unit]
Description     = besu eth1 service
Wants           = network-online.target
After           = network-online.target 

[Service]
User            = $(whoami)
ExecStart       = $(echo $HOME)/besu/bin/besu --metrics-enabled --rpc-http-enabled --data-path="$HOME/.besu"
Restart         = on-failure
RestartSec      = 3

[Install]
WantedBy    = multi-user.target
EOF
```

Mueva el archivo de unidad a `/etc/systemd/system` y otorgue permisos.

```bash
sudo mv $HOME/eth1.service /etc/systemd/system/eth1.service
```

```bash
sudo chmod 644 /etc/systemd/system/eth1.service
```

Ejecute lo siguiente para habilitar auto-inicio en el momento de arranque.

```text
sudo systemctl daemon-reload
sudo systemctl enable eth1
```

#### ⛓ Iniciar besu

```text
sudo systemctl start eth1
```
{% endtab %}

{% tab title="Nethermind" %}
{% hint style="info" %}
**La mente** es un cliente de bandera Ethereum todo acerca del rendimiento y la flexibilidad. Construido en **. ET** núcleo, una plataforma muy amplia, amigable con el aliento, la mente hace que la integración con las infraestructuras existentes sea sencilla, sin perder de vista la estabilidad, la fiabilidad, la integridad de los datos y la seguridad.
{% endhint %}

#### ⚙ Instalar dependencias

```text
sudo apt-get update
sudo apt-get install curl libsnappy-dev libc6-dev jq libc6 unzip -y
```

#### 🌜 Descargar y descomprimir la mente

Revise la última versión en [https://github.com/\)\[video\] mindEth/nethermind/releases](https://github.com/NethermindEth/nethermind/releases)

Descargue automáticamente la última versión de linux, des-zip y limpieza.

```bash
mkdir $HOME/nethermind
chmod 775 $HOME/nethermind
cd $HOME/nethermind
curl -s https://api.github.com/repos/NethermindEth/nethermind/releases/latest | jq -r ".assets[] | select(.name) | .browser_download_url" | grep linux  | xargs wget -q --show-progress
unzip -o nethermind*.zip
rm nethermind*linux*.zip
```

⚙ **Configurar y configurar el sistema**

Ejecute lo siguiente para crear un **archivo de unidad** para definir su configuración `eth1.service`.

Simplemente copia/pega lo siguiente.

```bash
cat > $HOME/eth1.service << EOF 
[Unit]
Description     = nethermind eth1 service
Wants           = network-online.target
After           = network-online.target 

[Service]
User            = $(whoami)
ExecStart       = $(echo $HOME)/nethermind/Nethermind.Runner --baseDbPath $HOME/.nethermind --Metrics.Enabled true --JsonRpc.Enabled true --Sync.DownloadBodiesInFastSync true --Sync.DownloadReceiptsInFastSync true --Sync.AncientBodiesBarrier 11052984 --Sync.AncientReceiptsBarrier 11052984
Restart         = on-failure
RestartSec      = 3

[Install]
WantedBy    = multi-user.target
EOF
```

Mueva el archivo de unidad a `/etc/systemd/system` y otorgue permisos.

```bash
sudo mv $HOME/eth1.service /etc/systemd/system/eth1.service
```

```bash
sudo chmod 644 /etc/systemd/system/eth1.service
```

Ejecute lo siguiente para habilitar auto-inicio en el momento de arranque.

```text
sudo systemctl daemon-reload
sudo systemctl enable eth1
```

#### ⛓ Iniciar la mente

```text
sudo systemctl start eth1
```
{% endtab %}

{% tab title="Configuración mínima de hardware \(Infura\)" %}
{% hint style="info" %}
Infura es adecuada para configuraciones de espacio limitado. Ejecute siempre su propio nodo eth1 completo cuando sea posible.
{% endhint %}

Regístrate para obtener una clave de acceso API en [https://infura.io/](https://infura.io/)

1. Regístrese para obtener una cuenta gratuita.
2. Confirme su dirección de correo electrónico.
3. Visita tu panel de control [https://infura.io/dashboard](https://infura.io/dashboard)
4. Crear un proyecto, darle un nombre.
5. Seleccione **Mainnet** como ENDPOINT
6. Siga la configuración específica para su cliente eth2 que se encuentra a continuación.

{% hint style="success" %}
También utiliza un nodo Ethereum gratuito en [https://ethereumnodes.com/](https://ethereumnodes.com/)
{% endhint %}

## Configuración específica de Nimbus

1. Al crear el **archivo de unidad**de su sistema, actualice el parámetro `--web-url` con este punto final.
2. Copiar el punto final del websocket. Comienza con `wss://`
3. Guarde esto para el paso 4, configurando su nodo eth2.

```bash
#ejemplo
--web3-url=<your wss:// infura endpoint>
```

## Configuración específica de Teku

1. Después de crear el `teku.yaml` ubicado en `mañana/teku/teku.yaml`, actualiza el parámetro `--eth1-endpoint` con este endpoint.
2. Copiar el punto final http. Comienza con `http://`
3. Guarde esto para el paso 4, configurando su nodo eth2.

```bash
#ejemplo
eth1-endpoint: <your https:// infura endpoint>
```

## Configuración Específica del Faro

1. Al crear su **sistema de cadena de beacon** **archivo unitario**, agregue el parámetro `--eth1-endpoint` con este endpoint.
2. Copia el punto final **https**. Comienza con `https://`
3. Guarde esto para el paso 4, configurando su nodo eth2.

```bash
#ejemplo
--eth1-endpoint=<your https:// infura endpoint>
```

## Configuración específica del Prysm

1. Al crear su **archivo de unidad de sistema de cadena de beacon**, actualice el parámetro `--http-web3provider` con este endpoint.
2. Copia el punto final **https**. Comienza con `https://`
3. Guarde esto para el paso 4, configurando su nodo eth2.

```bash
#ejemplo
--http-web3provider=<your https:// infura endpoint>
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
La sincronización de un nodo eth1 puede tardar hasta 1 semana. En máquinas de alta gama con internet gigabit, se espera que la sincronización tome menos de un día.
{% endhint %}

{% hint style="success" %}
Su nodo eth1 está completamente sincronizado cuando se producen estos eventos.

* **`OpenEthereum:`** `Imported #<block number>`
* **`Geth:`** `Importado nuevo segmento de cadena`
* **`Besu:`** `Importado #<block number>`
* **`mente:`** `Ya no sincronizando Cabeceras Antiguas`
{% endhint %}

#### 🛠 Comandos útiles de eth1.service

🗒 **Para ver y seguir los registros eth1**

```text
journalctl -u eth1 -f
```

🗒 **Para detener el servicio eth1**

```text
sudo systemctl stop eth1
```

## 🌜 4. Configurar un nodo y validador de la cadena ETH2

Su elección de Lighthouse, Nimbus, Teku, Prysm o Lodestar.

{% tabs %}
{% tab title="Lighthouse" %}
{% hint style="info" %}
[Lighthouse](https://github.com/sigp/lighthouse) es un cliente Eth2.0 centrado en la velocidad y la seguridad. El equipo detrás de ella, [Sigma Prime](https://sigmaprime.io/), es una empresa de seguridad e ingeniería de software que ha financiado Lighthouse junto con la Fundación Ethereum, Consensys, y particulares. Lighthouse está compilado en Rust y se ofrece bajo una licencia Apache 2.0.
{% endhint %}

## ⚙ 4.1. Instalar dependencia de rust

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Introduzca '1' para continuar con la instalación por defecto.

Actualice sus variables de entorno.

```bash
echo export PATH="$HOME/.cargo/bin:$PATH" >> ~/.bashrc
source ~/.bashrc
```

Instalar dependencias de rust.

```text
sudo apt-get update
sudo apt install -y git gcc g++ make cmake pkg-config libssl-dev
```

## 💡 4.2. Construir Faro desde la fuente

```bash
mkdir ~/git
cd ~/git
git clone https://github.com/sigp/lighthouse.git
cd lighthouse
git fetch --all && git checkout stable && git pull
make
```

{% hint style="info" %}
En caso de errores de compilación, ejecute la siguiente secuencia.

```text
rustup update
cargo clean
make
```
{% endhint %}

{% hint style="info" %}
Este proceso de compilación puede tardar unos minutos.
{% endhint %}

Verifique que el faro se ha instalado correctamente comprobando el número de versión.

```text
lighthouse --version
```

## 🎩 4.3. Importar clave de validador

{% hint style="info" %}
Cuando importas tus claves en Lighthouse, las claves de tu validador\(s\) se almacenan en la carpeta `$HOME/.lighthouse/mainnet/validators`.
{% endhint %}

Ejecute el siguiente comando para importar sus claves de validador desde el directorio de herramientas eth2deposit-cli.

Introduzca la contraseña de su almacén de claves para importar cuentas.

```bash
lighthouse account validator import --network mainnet --directory=$HOME/eth2deposit-cli/validator_keys
```

Verifique que las cuentas se han importado correctamente.

```bash
lighthouse account_manager validator list --network mainnet
```

{% hint style="danger" %}
**ADVERTENCIA**: NO UTILICE LOS KEYSTORES ORIGINALES PARA VALIDAR CON OTROS CLIENTOS, O USTED SERÁ SLASHADO.
{% endhint %}

## 🔥 4.4. Configurar desvío de puertos y/o firewall

Específicamente para su configuración de red o configuración de proveedores de nube, [asegúrese de que los puertos firewall de su validador están abiertos y alcanzables.](guide-or-security-best-practices-for-a-eth2-validator-beaconchain-node.md#configure-your-firewall)

* **Lighthouse beacon chain** requiere el puerto 9000 para tcp y udp
* **eth1** node requiere el puerto 30303 para tcp y udp

{% hint style="info" %}
✨ **Consejo de reenvío de puertos:** Tendrás que redirigir y abrir puertos a tu validador. Verifique que está trabajando con [https://www.yougetsignal.com/tools/open-ports/](https://www.yougetsignal.com/tools/open-ports/) o [https://canyouseeme.org/](https://canyouseeme.org/).
{% endhint %}

## ⛓ 4.5. Iniciar la cadena del faro

#### 🍰 Beneficios de usar systemd para su cadena de balizas <a id="benefits-of-using-systemd-for-your-stake-pool"></a>

1. Iniciar automáticamente su cadena de faros cuando el ordenador se reinicia debido al mantenimiento, interrupción de energía, etc.
2. Reinicie automáticamente los procesos de la cadena de baliza bloqueada.
3. Maximice su tiempo de actividad y rendimiento de la cadena de balizas.

#### 🛠 Instrucciones de configuración para el sistema

Ejecute lo siguiente para crear un **archivo de unidad** para definir su configuración`beacon-chain.service`. Simplemente copie y pegue.

```bash
cat > $HOME/beacon-chain.service << EOF 
# The eth2 beacon chain service (part of systemd)
# file: /etc/systemd/system/beacon-chain.service 

[Unit]
Description     = eth2 beacon chain service
Wants           = network-online.target
After           = network-online.target 

[Service]
User            = $(whoami)
ExecStart       = $(which lighthouse) bn --staking --validator-monitor-auto --metrics --network mainnet
Restart         = on-failure

[Install]
WantedBy    = multi-user.target
EOF
```

{% hint style="info" %}
\*\*\*\*\*🔥 **Lighthouse Pro Tip:** En la línea **ExecStart** , añadir la bandera `--eth1-endpoints` permite redundantes nodos eth1. Separar con comas. Asegúrate de que el endpoint no termina con una barra final o`/` Quitarlo.

```bash
# Ejemplo:
--eth1-endpoints http://localhost:8545,https://nodes.mewapi.io/rpc/eth,https://mainnet.eth.cloud.ava.do,https://mainnet.infura.io/v3/xxx
```
{% endhint %}

Mover el archivo de unidad a `/etc/systemd/system`

```bash
sudo mv $HOME/beacon-chain.service /etc/systemd/system/beacon-chain.service
```

Actualizar permisos de archivo.

```bash
sudo chmod 644 /etc/systemd/system/beacon-chain.service
```

Ejecute lo siguiente para habilitar auto-start al momento de arranque y luego inicie su servicio de nodo beacon.

```text
sudo systemctl daemon-reload
sudo systemctl enable beacon-chain
sudo systemctl start beacon-chain
```

{% hint style="info" %}
**Resolución de problemas comunes**:

_La cadena de faros no se pudo conectar al servicio :8545?_

* En el archivo de unidad de cadena beacon bajo \[Service\], añadido, "`ExecStartPre = /bin/sleep 30`" para que espere 30 segundos a que se inicie el nodo eth1 antes de conectarse.

_CRIT id de cadena eth1 no válido. Por favor, cambie al id de cadena correcto._

* Permitir que su nodo eth1 sincronice completamente con mainnet.
{% endhint %}

{% hint style="success" %}
Buen trabajo. Su cadena de faros está ahora gestionada por la fiabilidad y robustez del sistema. Debajo hay algunos comandos para usar el sistema.
{% endhint %}

### 🛠 Algunos comandos útiles del sistema

#### ✅ Comprueba si la cadena de baliza está activa

```text
sudo systemctl is-active beacon-chain
```

#### 🔎 Ver el estado de la cadena del faro

```text
sudo systemctl status beacon-chain
```

#### 🔄 Reiniciando la cadena del faro

```text
sudo systemctl reload-or-restart beacon-chain
```

#### 🛑 Detener la cadena del faro

```text
sudo systemctl stop beacon-chain
```

#### :file\_gabinet: Ver y filtrar registros

```bash
#ver y seguir el registro
journalctl --unit=beacon-chain -f
#ver registro desde ayer
journalctl --unit=beacon-chain --since=yesterday
#ver registro desde hoy
journalctl --unit=beacon-chain --since=today
#ver registro entre una fecha
journalctl --unit=beacon-chain --since='2020-12-01 00:00:00' --until='2020-12-02 12:00:00'
```

## 🧬 4.6. Iniciar el validador

#### 🚀 Configurar Graffiti y POAP

Configure su `graffiti`, un mensaje personalizado incluido en los bloques que su validador propone con éxito, y gane un token POAP. [Genera tu cadena POAP suministrando una dirección de Ethereum 1.0 aquí.](https://beaconcha.in/poap)

Ejecute el siguiente comando para establecer la variable `MY_GRAFFITI`. Reemplazar `<my POAP string or message>` entre las comillas simples.

```bash
MY_GRAFFITI='<my POAP string or message>'
# Ejemplos
# MY_GRAFFITI='poapAAAAACGatUA1bLuDnL4FMD13BfoD'
# MY_GRAFFITI='eth2 rulez!'
```

{% hint style="info" %}
Aprende más sobre [POAP - La ficha de prueba de asistencia. ](https://www.poap.xyz/)
{% endhint %}

#### 🍰 Beneficios de usar systemd para su validador <a id="benefits-of-using-systemd-for-your-stake-pool"></a>

1. Iniciar automáticamente el validador cuando el ordenador se reinicia debido al mantenimiento, interrupción de energía, etc.
2. Reiniciar automáticamente los procesos validadores bloqueados.
3. Maximice su validador a tiempo de espera y rendimiento.

#### 🛠 Instrucciones de configuración para el sistema

Ejecute lo siguiente para crear un **archivo de unidad** para definir su configuración`validator.service`. Simplemente copie y pegue.

```bash
cat > $HOME/validator.service << EOF 
# The eth2 validator service (part of systemd)
# file: /etc/systemd/system/validator.service 

[Unit]
Description     = eth2 validator service
Wants           = network-online.target beacon-chain.service
After           = network-online.target 

[Service]
User            = $(whoami)
ExecStart       = $(which lighthouse) vc --network mainnet --graffiti "${MY_GRAFFITI}" --metrics 
Restart         = on-failure

[Install]
WantedBy    = multi-user.target
EOF
```

Mover el archivo de unidad a `/etc/systemd/system`

```bash
sudo mv $HOME/validator.service /etc/systemd/system/validator.service
```

Actualizar permisos de archivo.

```bash
sudo chmod 644 /etc/systemd/system/validator.service
```

Ejecute lo siguiente para habilitar auto-inicio al momento de arranque y luego inicie su validador.

```text
sudo systemctl daemon-reload
sudo systemctl enable validator
sudo systemctl start validator
```

{% hint style="success" %}
Buen trabajo. Su validador ahora está gestionado por la fiabilidad y robustez del sistema. Debajo hay algunos comandos para usar el sistema.
{% endhint %}

### 🛠 Algunos comandos útiles del sistema

#### ✅ Comprueba si el validador está activo

```text
sudo systemctl is-active validator
```

#### 🔎 Ver el estado del validador

```text
sudo systemctl status validator
```

#### 🔄 Reiniciando el validador

```text
sudo systemctl reload-or-restart validator
```

#### 🛑 Detener el validador

```text
sudo systemctl stop validator
```

#### Ver y filtrar registros

```bash
#ver y seguir el registro
journalctl --unit=validator -f
#ver registro desde ayer
journalctl --unit=validator --since=yesterday
#ver registro desde hoy
journalctl --unit=validator --since=today
#ver registro entre una fecha
journalctl --unit=validator --since='2020-12-01 00:00:00' --until='2020-12-02 12:00:00'
```
{% endtab %}

{% tab title="Nimbus" %}
{% hint style="info" %}
[Nimbus](https://our.status.im/tag/nimbus/) es un proyecto de investigación y una implementación de cliente para Ethereum 2. diseñado para funcionar bien en sistemas embebidos y dispositivos móviles personales, incluyendo smartphones antiguos con hardware restringido a recursos. El equipo de Nimbus es de [Estado](https://status.im/about/) la empresa más conocida por [su navegador de mensajeras/wallet/Web3](https://status.im/) con el mismo nombre. Nimbus \(Apache 2\) está escrito en Nim, un lenguaje con sintaxis tipo Python que compila a C.
{% endhint %}

## ⚙ 4.1. Construir Nimbus desde la fuente

Instalar dependencias.

```text
sudo apt-get update
sudo apt-get install curl build-essential git -y
```

Instalar y construir Nimbus.

```bash
mkdir ~/git 
cd ~/git
git clone https://github.com/status-im/nimbus-eth2
cd nimbus-eth2
make NIMFLAGS="-d:insecure" nimbus_beacon_node
```

{% hint style="info" %}
El proceso de compilación puede tardar unos minutos.
{% endhint %}

Verifique que Nimbus se ha instalado correctamente mostrando la ayuda.

```bash
cd $HOME/git/nimbus-eth2/build
./nimbus_beacon_node --help
```

Copia el archivo binario a `/usr/bin`

```bash
sudo cp $HOME/git/nimbus-eth2/build/nimbus_beacon_node /usr/bin
```

## 🎩 4.2. Importar clave de validador <a id="6-import-validator-key"></a>

Crear una estructura de directorio para almacenar datos de nimbus.

```bash
sudo mkdir -p /var/lib/nimbus
```

Tomar posesión de este directorio y establecer el nivel de permisos correcto.

```bash
sudo chown $(whoami):$(whoami) /var/lib/nimbus
sudo chmod 700 /var/lib/nimbus
```

El siguiente comando importará sus claves de validador.

Introduzca la contraseña de su almacén de claves para importar cuentas.

```bash
cd $HOME/git/nimbus-eth2
build/nimbus_beacon_node deposits import --data-dir=/var/lib/nimbus $HOME/eth2deposit-cli/validator_keys
```

Ahora puede verificar que las cuentas fueron importadas con éxito haciendo un listado de directorios.

```bash
ll /var/lib/nimbus/validators
```

Debería ver una carpeta llamada para cada una de las pubkey de su validador.

{% hint style="info" %}
Cuando importas tus claves en Nimbus, las claves de tu validador\(s\) se almacenan en la carpeta `/var/lib/nimbus` , bajo `secretos` y `validadores.`

La carpeta `secrets` contiene el secreto común que le da acceso a todas sus claves de validador.

La carpeta `validators` contiene su almacén de claves\(s\) \\(claves cifradas\\). Los validadores utilizan los almacenes de claves como método para el intercambio de claves.

Para más información sobre claves y tiendas de claves, consulte [aquí](https://blog.ethereum.org/2020/05/21/keys/).
{% endhint %}

{% hint style="danger" %}
**ADVERTENCIA**: NO UTILICE LOS KEYSTORES ORIGINALES PARA VALIDAR CON OTROS CLIENTOS, O USTED SERÁ SLASHADO.
{% endhint %}

## 🔥 4.3. Configurar desvío de puertos y/o firewall

Específicamente para su configuración de red o configuración de proveedores de nube, [asegúrese de que los puertos firewall de su validador están abiertos y alcanzables.](guide-or-security-best-practices-for-a-eth2-validator-beaconchain-node.md#configure-your-firewall)

* **Nimbus nodo de cadena de baliza** usará el puerto 9000 para tcp y udp
* **eth1** node requiere el puerto 30303 para tcp y udp

{% hint style="info" %}
✨ **Consejo de reenvío de puertos:** Tendrás que redirigir y abrir puertos a tu validador. Verifique que está trabajando con [https://www.yougetsignal.com/tools/open-ports/](https://www.yougetsignal.com/tools/open-ports/) o [https://canyouseeme.org/](https://canyouseeme.org/).
{% endhint %}

## 🏂 4.4. Iniciar la cadena del faro y validador

{% hint style="info" %}
Nimbus combina tanto la cadena de baliza como el validador en un solo proceso.
{% endhint %}

#### 🚀 Configurar Graffiti y POAP

Configure su `graffiti`, un mensaje personalizado incluido en los bloques que su validador propone con éxito, y gane un token POAP. [Genera tu cadena POAP suministrando una dirección de Ethereum 1.0 aquí.](https://beaconcha.in/poap)

Ejecute el siguiente comando para establecer la variable `MY_GRAFFITI`. Reemplazar `<my POAP string or message>` entre las comillas simples.

```bash
MY_GRAFFITI='<my POAP string or message>'
# Ejemplos
# MY_GRAFFITI='poapAAAAACGatUA1bLuDnL4FMD13BfoD'
# MY_GRAFFITI='eth2 rulez!'
```

{% hint style="info" %}
Aprende más sobre [POAP - La ficha de prueba de asistencia. ](https://www.poap.xyz/)
{% endhint %}

#### 🍰 Benefits of using systemd for your beacon chain and validator <a id="benefits-of-using-systemd-for-your-stake-pool"></a>

1. Iniciar automáticamente su cadena de faros cuando el ordenador se reinicia debido al mantenimiento, interrupción de energía, etc.
2. Reinicie automáticamente los procesos de la cadena de baliza bloqueada.
3. Maximice su tiempo de actividad y rendimiento de la cadena de balizas.

#### 🛠 Instrucciones de configuración

Ejecute lo siguiente para crear un **archivo de unidad** para definir su configuración`beacon-chain.service`. Simplemente copie y pegue.

```bash
cat > $HOME/beacon-chain.service << EOF 
# The eth2 beacon chain service (part of systemd)
# file: /etc/systemd/system/beacon-chain.service 

[Unit]
Description     = eth2 beacon chain service
Wants           = network-online.target
After           = network-online.target 

[Service]
Type            = simple
User            = $(whoami)
WorkingDirectory= /var/lib/nimbus
ExecStart       = /bin/bash -c '/usr/bin/nimbus_beacon_node --network=mainnet --graffiti="${MY_GRAFFITI}" --data-dir=/var/lib/nimbus --web3-url=ws://127.0.0.1:8546 --metrics --metrics-port=8008 --rpc --rpc-port=9091 --validators-dir=/var/lib/nimbus/validators --secrets-dir=/var/lib/nimbus/secrets --log-file=/var/lib/nimbus/beacon.log'
Restart         = on-failure

[Install]
WantedBy    = multi-user.target
EOF
```

{% hint style="warning" %}
Nimbus sólo soporta conexiones websocket \("ws://" y "wss://"\) para el nodo ETH1. Geth, OpenEthereum, Infura and Chainstack ETH1 nodes are verified compatible.
{% endhint %}

Mover el archivo de unidad a `/etc/systemd/system`

```bash
sudo mv $HOME/beacon-chain.service /etc/systemd/system/beacon-chain.service
```

Actualizar permisos de archivo.

```bash
sudo chmod 644 /etc/systemd/system/beacon-chain.service
```

Ejecute lo siguiente para habilitar auto-start al momento de arranque y luego inicie su servicio de nodo beacon.

```text
sudo systemctl daemon-reload
sudo systemctl enable beacon-chain
sudo systemctl start beacon-chain
```

{% hint style="success" %}
Buen trabajo. Su cadena de faros está ahora gestionada por la fiabilidad y robustez del sistema. Debajo hay algunos comandos para usar el sistema.
{% endhint %}

### 🛠 Algunos comandos útiles del sistema

#### ✅ Comprueba si la cadena de baliza está activa

```text
sudo systemctl is-active beacon-chain
```

#### 🔎 Ver el estado de la cadena del faro

```text
sudo systemctl status beacon-chain
```

#### 🔄 Reiniciando la cadena del faro

```text
sudo systemctl reload-or-restart beacon-chain
```

#### 🛑 Detener la cadena del faro

```text
sudo systemctl stop beacon-chain
```

#### Ver y filtrar registros

```bash
#ver y seguir el registro
journalctl --unit=beacon-chain -f
#ver registro desde ayer
journalctl --unit=beacon-chain --since=yesterday
#ver registro desde hoy
journalctl --unit=beacon-chain --since=today
#ver registro entre una fecha
journalctl --unit=beacon-chain --since='2020-12-01 00:00:00' --until='2020-12-02 12:00:00'
```
{% endtab %}

{% tab title="Teku" %}
{% hint style="info" %}
[PegaSys Teku](https://pegasys.tech/teku/) \(antes conocido como Artemis\) es un cliente basado en Java Ethereum 2.0 diseñado & construido para satisfacer las necesidades institucionales y los requisitos de seguridad. PegaSys es un brazo de [ConsenSys](https://consensys.net/) dedicado a la construcción de clientes y herramientas listas para interactuar con la plataforma de Ethereum del núcleo. Teku tiene licencia Apache 2 y está escrito en Java, un lenguaje notable por su autenticidad & ubicación.
{% endhint %}

## ⚙ 4.1 Construir Teku desde el origen

Install git.

```text
sudo apt-get install git -y
```

Instalar Java 11.

Para **Ubuntu 20.x**, utiliza lo siguiente

```text
sudo apt update
sudo apt install openjdk-11-jdk -y
```

Para **Ubuntu 18.x**, utiliza lo siguiente

```text
sudo add-apt-repository ppa:linuxuprising/java
sudo apt update
sudo apt install oracle-java11-set-default -y
```

Verifique que Java 11+ está instalado.

```bash
java --version
```

Instalar y compilar Teku.

```bash
mkdir ~/git
cd ~/git
git clone https://github.com/ConsenSys/teku.git
cd teku
./gradlew distTar installDist
```

{% hint style="info" %}
Este proceso de compilación puede tardar unos minutos.
{% endhint %}

Verifique que Teku se ha instalado correctamente al mostrar la versión.

```bash
cd $HOME/git/teku/build/install/teku/bin
./teku --version
```

Copie el archivo binario teku a `/usr/bin/teku`

```bash
sudo cp -r $HOME/git/teku/build/install/teku /usr/bin/teku
```

## 🔥 4.2. Configurar desvío de puertos y/o firewall

Específicamente para su configuración de red o configuración de proveedores de nube, [asegúrese de que los puertos firewall de su validador están abiertos y alcanzables.](guide-or-security-best-practices-for-a-eth2-validator-beaconchain-node.md#configure-your-firewall)

* **El nodo de cadena de baliza Teku** usará el puerto 9000 para tcp y udp
* **eth1** node requiere el puerto 30303 para tcp y udp

{% hint style="info" %}
✨ **Consejo de reenvío de puertos:** Tendrás que redirigir y abrir puertos a tu validador. Verifique que está trabajando con [https://www.yougetsignal.com/tools/open-ports/](https://www.yougetsignal.com/tools/open-ports/) o [https://canyouseeme.org/](https://canyouseeme.org/).
{% endhint %}

## 🏂 4.3. Configurar la cadena del faro y el validador

{% hint style="info" %}
Teku combina tanto la cadena de baliza como el validador en un solo proceso.
{% endhint %}

Configurar una estructura de directorios para Teku.

```bash
sudo mkdir -p /var/lib/teku
sudo mkdir -p /etc/teku
sudo chown $(whoami):$(whoami) /var/lib/teku
```

Copie el directorio `validator_files` al directorio de datos que creamos arriba y elimine el archivo de deposit\_data adicional.

```bash
cp -r $HOME/eth2deposit-cli/validator_keys /var/lib/teku
rm /var/lib/teku/validator_keys/deposit_data*
```

{% hint style="danger" %}
**ADVERTENCIA**: NO UTILICE LOS KEYSTORES ORIGINALES PARA VALIDAR CON OTROS CLIENTOS, O USTED SERÁ SLASHADO.
{% endhint %}

Almacena la contraseña de tu validador en un archivo.

Actualiza tu contraseña entre las comillas después de `echo`.

```bash
echo 'my_password_goes_here' > $HOME/validators-password.txt
sudo mv $HOME/validators-password.txt /etc/teku/validators-password.txt
sudo chmod 600 /etc/teku/validators-password.txt
```

#### 🚀 Configurar Graffiti y POAP

Configure su `graffiti`, un mensaje personalizado incluido en los bloques que su validador propone con éxito, y gane un token POAP. [Genera tu cadena POAP suministrando una dirección de Ethereum 1.0 aquí.](https://beaconcha.in/poap)

Ejecute el siguiente comando para establecer la variable `MY_GRAFFITI`. Reemplazar `<my POAP string or message>` entre las comillas simples.

```bash
MY_GRAFFITI='<my POAP string or message>'
# Examples
# MY_GRAFFITI='poapAAAAACGatUA1bLuDnL4FMD13BfoD'
# MY_GRAFFITI='eth2 rulez!'
```

{% hint style="info" %}
Aprende más sobre [POAP - La ficha de prueba de asistencia. ](https://www.poap.xyz/)
{% endhint %}

Genera tu archivo de configuración Teku. Simplemente copie y pegue.

```bash
cat > $HOME/teku.yaml << EOF
# network
network: "mainnet"

# p2p
p2p-enabled: true
p2p-port: 9000
# validators
validator-keys: "/var/lib/teku/validator_keys:/var/lib/teku/validator_keys"
validators-graffiti: "${MY_GRAFFITI}"

# Eth 1
eth1-endpoint: "http://localhost:8545"

# metrics
metrics-enabled: true
metrics-port: 8008

# database
data-path: "$(echo $HOME)/tekudata"
data-storage-mode: "archive"

# rest api
rest-api-port: 5051
rest-api-docs-enabled: true
rest-api-enabled: true

# logging
log-include-validator-duties-enabled: true
log-destination: CONSOLE
EOF
```

Mover el archivo de configuración a `etc/teku`

```bash
sudo mv $HOME/teku.yaml /etc/teku/teku.yaml
```

## 🎩 Clave validadora de importación 4.4

{% hint style="info" %}
Al especificar los directorios para sus claves validadoras, Teku espera encontrar archivos de claves y contraseñas con el mismo nombre.

Por ejemplo `keystore-m_12221_3600_1_0_0-11222333.json` y `keystore-m_12221_3600_1_0_0-11222333.txt`
{% endhint %}

Crea un archivo de contraseña correspondiente para cada uno de tus validadores.

```bash
for f in /var/lib/teku/validator_keys/keystore*.json; do cp /etc/teku/validators-password.txt /var/lib/teku/validator_keys/$(basename $f .json).txt; done
```

Verificar que el almacén de claves de su validador y las contraseñas del validador estén presentes comprobando el siguiente directorio.

```bash
ll /var/lib/teku/validator_keys
```

## 🏁 4.5. Iniciar la cadena del faro y validador

Use **systemd** para gestionar el inicio y la detención del teku.

#### 🍰 Benefits of using systemd for your beacon chain and validator <a id="benefits-of-using-systemd-for-your-stake-pool"></a>

1. Iniciar automáticamente su cadena de faros cuando el ordenador se reinicia debido al mantenimiento, interrupción de energía, etc.
2. Reinicie automáticamente los procesos de la cadena de baliza bloqueada.
3. Maximice su tiempo de actividad y rendimiento de la cadena de balizas.

#### 🛠 Instrucciones de configuración

Ejecute lo siguiente para crear un **archivo de unidad** para definir su configuración`beacon-chain.service`.

```bash
cat > $HOME/beacon-chain.service << EOF
# The eth2 beacon chain service (part of systemd)
# file: /etc/systemd/system/beacon-chain.service 

[Unit]
Description     = eth2 beacon chain service
Wants           = network-online.target
After           = network-online.target 

[Service]
User            = $(whoami)
ExecStart       = /usr/bin/teku/bin/teku -c /etc/teku/teku.yaml
Restart         = on-failure
Environment     = JAVA_OPTS=-Xmx5g

[Install]
WantedBy	= multi-user.target
EOF
```

Mover el archivo de unidad a `/etc/systemd/system`

```bash
sudo mv $HOME/beacon-chain.service /etc/systemd/system/beacon-chain.service
```

Actualizar permisos de archivo.

```bash
sudo chmod 644 /etc/systemd/system/beacon-chain.service
```

Ejecute lo siguiente para habilitar auto-start al momento de arranque y luego inicie su servicio de nodo beacon.

```text
sudo systemctl daemon-reload
sudo systemctl enable beacon-chain
sudo systemctl start beacon-chain
```

{% hint style="success" %}
Buen trabajo. Su cadena de faros está ahora gestionada por la fiabilidad y robustez del sistema. Debajo hay algunos comandos para usar el sistema.
{% endhint %}

### 🛠 Algunos comandos útiles del sistema

#### ✅ Comprueba si la cadena de baliza está activa

```text
sudo systemctl is-active beacon-chain
```

#### 🔎 Ver el estado de la cadena del faro

```text
sudo systemctl status beacon-chain
```

#### 🔄 Reiniciando la cadena del faro

```text
sudo systemctl reload-or-restart beacon-chain
```

#### 🛑 Detener la cadena del faro

```text
sudo systemctl stop beacon-chain
```

#### :file\_gabinet: Ver y filtrar registros

```bash
#ver y seguir el registro
journalctl --unit=beacon-chain -f
#ver registro desde ayer
journalctl --unit=beacon-chain --since=yesterday
#ver registro desde hoy
journalctl --unit=beacon-chain --since=today
#ver registro entre una fecha
journalctl --unit=beacon-chain --since='2020-12-01 00:00:00' --until='2020-12-02 12:00:00'
```
{% endtab %}

{% tab title="Prysm" %}
{% hint style="info" %}
[Prysm](https://github.com/prysmaticlabs/prysm) es una implementación de Ethereum 2.0 protocolo con enfoque en usabilidad, seguridad y fiabilidad. Prysm es desarrollado por [Prysmatic Labs](https://prysmaticlabs.com/), una empresa con el único enfoque en el desarrollo de su cliente. Prysm está escrito en Go y publicado bajo una licencia GPL-3.0.
{% endhint %}

## ⚙ 4.1. Install Prysm

```bash
mkdir ~/prysm && cd ~/prysm 
curl https://raw.githubusercontent.com/prysmaticlabs/prysm/master/prysm.sh --output prysm.sh && chmod +x prysm.sh 
```

## 🔥 4.2. Configurar desvío de puertos y/o firewall

Específicamente para su configuración de red o configuración de proveedores de nube, [asegúrese de que los puertos firewall de su validador están abiertos y alcanzables.](guide-or-security-best-practices-for-a-eth2-validator-beaconchain-node.md#configure-your-firewall)

* **Prysm beacon chain node** usará el puerto 12000 para udp y el puerto 13000 para tcp
* **eth1** node requiere el puerto 30303 para tcp y udp

{% hint style="info" %}
✨ **Consejo de reenvío de puertos:** Tendrás que redirigir y abrir puertos a tu validador. Verifique que está trabajando con [https://www.yougetsignal.com/tools/open-ports/](https://www.yougetsignal.com/tools/open-ports/) o [https://canyouseeme.org/](https://canyouseeme.org/).
{% endhint %}

## 🎩 4.3. Importar clave de validador

Acepte los términos de uso, acepte la ubicación predeterminada de la billetera, introduzca una nueva contraseña para cifrar su billetera e introduzca la contraseña para sus cuentas importadas.

```bash
$HOME/prysm/prysm.sh validator accounts import --mainnet --keys-dir=$HOME/eth2deposit-cli/validator_keys
```

Verifique sus validadores importados con éxito.

```bash
$HOME/prysm/prysm.sh validator accounts list --mainnet
```

Confirme que las pubkeys de su validador están listadas.

> \#Salida de ejemplo:
>
> Mostrando 1 cuenta de validador Ver los datos de transacción de depósitos eth1 para sus cuentas ejecutando \`validator accounts list --show-deposit-data
>
> Cuenta 0 \| pens-herther-heat  
> \[validating public key\] 0x2374.....7121

{% hint style="danger" %}
**ADVERTENCIA**: NO UTILICE LOS KEYSTORES ORIGINALES PARA VALIDAR CON OTROS CLIENTOS, O USTED SERÁ SLASHADO.
{% endhint %}

## 🏂 4.4. Iniciar la cadena del faro

#### 🍰 Benefits of using systemd for your beacon chain and validator <a id="benefits-of-using-systemd-for-your-stake-pool"></a>

1. Iniciar automáticamente su cadena de faros cuando el ordenador se reinicia debido al mantenimiento, interrupción de energía, etc.
2. Reinicie automáticamente los procesos de la cadena de baliza bloqueada.
3. Maximice su tiempo de actividad y rendimiento de la cadena de balizas.

#### 🛠 Instrucciones de configuración

Ejecute lo siguiente para crear un **archivo de unidad** para definir su configuración`beacon-chain.service`. Simplemente copie y pegue.

```bash
cat > $HOME/beacon-chain.service << EOF 
# The eth2 beacon chain service (part of systemd)
# file: /etc/systemd/system/beacon-chain.service 

[Unit]
Description     = eth2 beacon chain service
Wants           = network-online.target
After           = network-online.target 

[Service]
Type            = simple
User            = $(whoami)
ExecStart       = $(echo $HOME)/prysm/prysm.sh beacon-chain --mainnet --p2p-max-peers=45 --http-web3provider=http://127.0.0.1:8545 --accept-terms-of-use 
Restart         = on-failure

[Install]
WantedBy    = multi-user.target
EOF
```

Mover el archivo de unidad a `/etc/systemd/system`

```bash
sudo mv $HOME/beacon-chain.service /etc/systemd/system/beacon-chain.service
```

Actualizar permisos de archivo.

```bash
sudo chmod 644 /etc/systemd/system/beacon-chain.service
```

Ejecute lo siguiente para habilitar auto-start al momento de arranque y luego inicie su servicio de nodo beacon.

```text
sudo systemctl daemon-reload
sudo systemctl enable beacon-chain
sudo systemctl start beacon-chain
```

{% hint style="success" %}
Buen trabajo. Su cadena de faros está ahora gestionada por la fiabilidad y robustez del sistema. Debajo hay algunos comandos para usar el sistema.
{% endhint %}

### 🛠 Algunos comandos útiles del sistema

#### ✅ Comprueba si la cadena de baliza está activa

```text
sudo systemctl is-active beacon-chain
```

#### 🔎 Ver el estado de la cadena del faro

```text
sudo systemctl status beacon-chain
```

#### 🔄 Reiniciando la cadena del faro

```text
sudo systemctl reload-or-restart beacon-chain
```

#### 🛑 Detener la cadena del faro

```text
sudo systemctl reload-or-restart beacon-chain
```

#### 🗒 Ver y filtrar registros

```bash
#ver y seguir el registro
journalctl --unit=beacon-chain -f
#ver registro desde ayer
journalctl --unit=beacon-chain --since=yesterday
#ver registro desde hoy
journalctl --unit=beacon-chain --since=today
#ver registro entre una fecha
journalctl --unit=beacon-chain -- e='2020-12-01 00:00:00' --until='2020-12-02 12:00'
```

## 🧬 4.5. Iniciar el validador <a id="9-start-the-validator"></a>

Almacena la contraseña de tu validador en un archivo y hazla de sólo lectura.

```bash
echo 'my_password_goes_here' > $HOME/.eth2validators/validators-password.txt
sudo chmod 600 $HOME/.eth2validators/validators-password.txt
```

#### 🚀 Configurar Graffiti y POAP

Configure su `graffiti`, un mensaje personalizado incluido en los bloques que su validador propone con éxito, y gane un token POAP. [Genera tu cadena POAP suministrando una dirección de Ethereum 1.0 aquí.](https://beaconcha.in/poap)

Ejecute el siguiente comando para establecer la variable `MY_GRAFFITI`. Reemplazar `<my POAP string or message>` entre las comillas simples.

```bash
MY_GRAFITI='<my POAP string or message>'
# Ejemplos
# MY_GRAFITI='poapAAAAACGatUA1bLuDnL4FMD13BfoD'
# MY_GRAFFITI='eth2 rulez!'
```

{% hint style="info" %}
Aprende más sobre [POAP - La ficha de prueba de asistencia. ](https://www.poap.xyz/)
{% endhint %}

Su elección de ejecutar un validador manualmente desde la línea de comandos o automáticamente con el sistema.

#### 🍰 Beneficios de usar systemd para su validador <a id="benefits-of-using-systemd-for-your-stake-pool"></a>

1. Iniciar automáticamente el validador cuando el ordenador se reinicia debido al mantenimiento, interrupción de energía, etc.
2. Reiniciar automáticamente los procesos validadores bloqueados.
3. Maximice su validador a tiempo de espera y rendimiento.

#### 🛠 Instrucciones de configuración para systemd

Ejecute lo siguiente para crear un **archivo de unidad** para definir su configuración`validator.service`. Simplemente copie y pegue.

```bash
cat > $HOME/validator.service << EOF 
# The eth2 validator service (part of systemd)
# file: /etc/systemd/system/validator.service 

[Unit]
Description     = eth2 validator service
Wants           = network-online.target beacon-chain.service
After           = network-online.target 

[Service]
User            = $(whoami)
ExecStart       = $(echo $HOME)/prysm/prysm.sh validator --mainnet --graffiti "${MY_GRAFFITI}" --accept-terms-of-use --wallet-password-file $(echo $HOME)/.eth2validators/validators-password.txt
Restart         = on-failure

[Install]
WantedBy	= multi-user.target
EOF
```

Mover el archivo de unidad a `/etc/systemd/system`

```bash
sudo mv $HOME/validator.service /etc/systemd/system/validator.service
```

Actualizar permisos de archivo.

```bash
sudo chmod 644 /etc/systemd/system/validator.service
```

Ejecute lo siguiente para habilitar auto-inicio al momento de arranque y luego inicie su validador.

```text
sudo systemctl daemon-reload
sudo systemctl enable validator
sudo systemctl start validator
```

### 🛠 Algunos comandos útiles del sistema

#### ✅ Comprueba si el validador está activo

```text
sudo systemctl is-active validator
```

#### 🔎 Ver el estado del validador

```text
sudo systemctl status validator
```

#### 🔄 Reiniciando el validador

```text
sudo systemctl reload-or-restart validator
```

#### 🛑 Detener el validador

```text
sudo systemctl stop validator
```

#### :file\_gabinet: Ver y filtrar registros

```bash
#ver y seguir el registro
journalctl --unit=validator -f
#ver registro desde ayer
journalctl --unit=validator --since=yesterday
#ver registro desde hoy
journalctl --unit=validator --since=today
#ver registro entre una fecha
journalctl --unit=validator --since='2020-12-01 00:00:00' --until='2020-12-02 12:00:00'
```
{% endtab %}

{% tab title="Lodestar" %}
{% hint style="info" %}
**Lodestar es una implementación de Typescript** de la especificación oficial [Ethereum 2.0](https://github.com/ethereum/eth2.0-specs) por el equipo [ChainSafe.io](https://lodestar.chainsafe.io/). Además del cliente de la cadena beacon, el equipo también está trabajando en 22 paquetes y bibliotecas. Puede encontrar una lista completa [aquí](https://hackmd.io/CcsWTnvRS_eiLUajr3gi9g). Por último, El equipo de Lodestar lidera el espacio Eth2 en investigación y desarrollo de clientes ligeros y ha recibido financiación de EF y Moloch DAO para este propósito.
{% endhint %}

## ⚙ 4.1 Construir Lodestar desde la fuente

Instalar curl y git.

```bash
sudo apt-get install gcc g++ make git curl -y
```

Instalar yarn.

```bash
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt update
sudo apt install yarn -y
```

Confirme que yarn está instalado correctamente.

```bash
yarn --version
# Debería mostrar la versión >= 1.22.4
```

Install nodejs.

```text
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
sudo apt-get install -y nodejs
```

Confirmar que los nodejs están instalados correctamente.

```bash
nodejs -v
# Debería mostrar la versión >= v12.18.3
```

Instalar y construir Lodestar.

```bash
mkdir ~/git
cd ~/git
git clone https://github.com/chainsafe/lodestar.git
cd lodestar
yarn install --ignore-optional
yarn run build
```

{% hint style="info" %}
Este proceso de compilación puede tardar unos minutos.
{% endhint %}

Verifique que Lodestar se ha instalado correctamente mostrando el menú de ayuda.

```text
./lodestar --help
```

## 🔥 4.2. Configurar desvío de puertos y/o firewall

Específicamente para su configuración de red o configuración de proveedores de nube, [asegúrese de que los puertos firewall de su validador están abiertos y alcanzables.](guide-or-security-best-practices-for-a-eth2-validator-beaconchain-node.md#configure-your-firewall)

* **El nodo de la cadena de baliza Lodestar** usará el puerto 30607 para tcp y el puerto 9000 para descubrimiento de pares udp.
* **eth1** node requiere el puerto 30303 para tcp y udp

{% hint style="info" %}
\*\*\*\*✨ **Consejo de reenvío de puertos:** Tendrás que redirigir y abrir puertos a tu validador. Verifique que está trabajando con [https://www.yougetsignal.com/tools/open-ports/](https://www.yougetsignal.com/tools/open-ports/) o [https://canyouseeme.org/](https://canyouseeme.org/).
{% endhint %}

## 🎩 4.3. Importar clave de validador

```bash
./lodestar account validator import \
  --network mainnet \
  --directory $HOME/eth2deposit-cli/validator_keys
```

Introduzca la contraseña de su almacén de claves para importar cuentas.

Confirme que sus claves fueron importadas correctamente.

```text
./lodestar account validator list --network mainnet
```

{% hint style="danger" %}
**ADVERTENCIA**: NO UTILICE LOS KEYSTORES ORIGINALES PARA VALIDAR CON OTROS CLIENTOS, O USTED SERÁ SLASHADO.
{% endhint %}

## 🏂 4.4. Iniciar la cadena del faro y validador

Ejecutar la cadena de baliza automáticamente con el sistema.

#### 🍰 Benefits of using systemd for your beacon chain <a id="benefits-of-using-systemd-for-your-stake-pool"></a>

1. Iniciar automáticamente su cadena de faros cuando el ordenador se reinicia debido al mantenimiento, interrupción de energía, etc.
2. Reinicie automáticamente los procesos de la cadena de baliza bloqueada.
3. Maximice su tiempo de actividad y rendimiento de la cadena de balizas.

#### 🛠 Instrucciones de configuración

Ejecute lo siguiente para crear un **archivo de unidad** para definir su configuración`beacon-chain.service`. Simplemente copie y pegue.

```bash
cat > $HOME/beacon-chain.service << EOF 
# The eth2 beacon chain service (part of systemd)
# file: /etc/systemd/system/beacon-chain.service 

[Unit]
Description     = eth2 beacon chain service
Wants           = network-online.target
After           = network-online.target 

[Service]
User            = $(whoami)
WorkingDirectory= $(echo $HOME)/git/lodestar
ExecStart       = $(echo $HOME)/git/lodestar/lodestar beacon --network mainnet --eth1.providerUrl http://localhost:8545 --metrics.enabled true --metrics.serverPort 8008
Restart         = on-failure

[Install]
WantedBy	= multi-user.target
EOF
```

Mover el archivo de unidad a `/etc/systemd/system`

```bash
sudo mv $HOME/beacon-chain.service /etc/systemd/system/beacon-chain.service
```

Actualizar permisos de archivo.

```bash
sudo chmod 644 /etc/systemd/system/beacon-chain.service
```

Ejecute lo siguiente para habilitar auto-start al momento de arranque y luego inicie su servicio de nodo beacon.

```text
sudo systemctl daemon-reload
sudo systemctl enable beacon-chain
sudo systemctl start beacon-chain
```

{% hint style="success" %}
Buen trabajo. Su cadena de faros está ahora gestionada por la fiabilidad y robustez del sistema. Debajo hay algunos comandos para usar el sistema.
{% endhint %}

### 🛠 Algunos comandos útiles del sistema

#### ✅ Comprueba si la cadena de baliza está activa

```text
sudo systemctl is-active beacon-chain
```

#### 🔎 Ver el estado de la cadena del faro

```text
sudo systemctl status beacon-chain
```

#### 🔄 Reiniciando la cadena del faro

```text
sudo systemctl reload-or-restart beacon-chain
```

#### 🛑 Detener la cadena del faro

```text
sudo systemctl stop beacon-chain
```

#### :file\_gabinet: Ver y filtrar registros

```bash
#ver y seguir el registro
journalctl --unit=beacon-chain -f
#ver registro desde ayer
journalctl --unit=beacon-chain --since=yesterday
#ver registro desde hoy
journalctl --unit=beacon-chain --since=today
#ver registro entre una fecha
journalctl --unit=beacon-chain --since='2020-12-01 00:00:00' --until='2020-12-02 12:00:00'
```

## 🧬 4.5. Iniciar el validador

#### 🚀 Configurar Graffiti y POAP

Configure su `graffiti`, un mensaje personalizado incluido en los bloques que su validador propone con éxito, y gane un token POAP. [Genera tu cadena POAP suministrando una dirección de Ethereum 1.0 aquí.](https://beaconcha.in/poap)

Ejecute el siguiente comando para establecer la variable `MY_GRAFFITI`. Reemplazar `<my POAP string or message>` entre las comillas simples.

```bash
MY_GRAFFITI='<my POAP string or message>'
# Ejemplos
# MY_GRAFFITI='poapAAAAACGatUA1bLuDnL4FMD13BfoD'
# MY_GRAFFITI='eth2 rulez!'
```

{% hint style="info" %}
Aprende más sobre [POAP - La ficha de prueba de asistencia. ](https://www.poap.xyz/)
{% endhint %}

Ejecute el validador automáticamente con el sistema.

#### 🍰 Beneficios de usar systemd para su validador <a id="benefits-of-using-systemd-for-your-stake-pool"></a>

1. Iniciar automáticamente el validador cuando el ordenador se reinicia debido al mantenimiento, interrupción de energía, etc.
2. Reiniciar automáticamente los procesos validadores bloqueados.
3. Maximice su validador a tiempo de espera y rendimiento.

#### 🛠 Instrucciones de configuración

Ejecute lo siguiente para crear un **archivo de unidad** para definir su configuración`validator.service`. Simplemente copie y pegue.

```bash
cat > $HOME/validator.service << EOF 
# The eth2 validator service (part of systemd)
# file: /etc/systemd/system/validator.service 

[Unit]
Description     = eth2 validator service
Wants           = network-online.target beacon-chain.service
After           = network-online.target 

[Service]
User            = $(whoami)
WorkingDirectory= $(echo $HOME)/git/lodestar
ExecStart       = $(echo $HOME)/git/lodestar/lodestar validator --network mainnet --graffiti "${MY_GRAFFITI}"
Restart         = on-failure

[Install]
WantedBy	= multi-user.target
EOF
```

Mover el archivo de unidad a `/etc/systemd/system`

```bash
sudo mv $HOME/validator.service /etc/systemd/system/validator.service
```

Actualizar permisos de archivo.

```bash
sudo chmod 644 /etc/systemd/system/validator.service
```

Ejecute lo siguiente para habilitar auto-inicio al momento de arranque y luego inicie su validador.

```text
sudo systemctl daemon-reload
sudo systemctl enable validator
sudo systemctl start validator
```

{% hint style="success" %}
Buen trabajo. Su validador ahora está gestionado por la fiabilidad y robustez del sistema. Debajo hay algunos comandos para usar el sistema.
{% endhint %}

### 🛠 Algunos comandos útiles del sistema

#### ✅ Comprueba si el validador está activo

```text
sudo systemctl is-active validator
```

#### 🔎 Ver el estado del validador

```text
sudo systemctl status validator
```

#### 🔄 Reiniciando el validador

```text
sudo systemctl reload-or-restart validator
```

#### 🛑 Detener el validador

```text
sudo systemctl stop validator
```

#### :file\_gabinet: Ver y filtrar registros

```bash
#ver y seguir el registro
journalctl --unit=validator -f
#ver registro desde ayer
journalctl --unit=validator --since=yesterday
#ver registro desde hoy
journalctl --unit=validator --since=today
#ver registro entre una fecha
journalctl --unit=validator --since='2020-12-01 00:00:00' --until='2020-12-02 12:00:00'
```
{% endtab %}
{% endtabs %}

## 🕒5. Sincronización de tiempo

{% hint style="info" %}
Debido a que la cadena de faros depende de tiempos precisos para realizar certificaciones y producir bloques, el tiempo de su computadora debe ser exacto a tiempo real NTP o NTS dentro de 0. segundos.
{% endhint %}

Configurar **Chrony** con la siguiente guía.

{% embed url="https://www.coincashew.com/coins/overview-ada/guide-how-to-build-a-haskell-stakepool-node/how-to-setup-chrony" %}

{% hint style="info" %}
chrony es una implementación del Protocolo de Tiempo de Red y ayuda a mantener el tiempo de su computadora sincronizado con NTP.
{% endhint %}

## 🔎6. Monitoreando a tu validador con Grafana y Prometeo

Prometheus es una plataforma de monitoreo que recolecta métricas de objetivos monitorizados mediante la eliminación de métricas HTTP en estos objetivos. [La documentación oficial está disponible aquí.](https://prometheus.io/docs/introduction/overview/) Grafana es un panel utilizado para visualizar los datos recolectados.

### 🐣 Instalación 6.1

Instale prometheus y prometheus node exporter.

```text
sudo apt-get install -y prometheus prometheus-node-exporter
```

Instalar grafana.

```bash
wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -
echo "deb https://packages.grafana.com/oss/deb stable main" > grafana.list
sudo mv grafana.list /etc/apt/sources.list.d/grafana.list
sudo apt-get update && sudo apt-get install -y grafana
```

Habilita los servicios para que se inicien automáticamente.

```bash
sudo systemctl enable grafana-server.service prometheus.service prometheus-node-exporter.service
```

Crea el archivo de configuración **prometheus.yml**. Elija la ficha para su cliente eth2. Simplemente copie y pegue.

{% tabs %}
{% tab title="Lighthouse" %}
```bash
cat > $HOME/prometheus.yml << EOF
global:
  scrape_interval:     15s # By default, scrape targets every 15 seconds.

  # Attach these labels to any time series or alerts when communicating with
  # external systems (federation, remote storage, Alertmanager).
  external_labels:
    monitor: 'codelab-monitor'

# A scrape configuration containing exactly one endpoint to scrape:
# Here it's Prometheus itself.
scrape_configs:
   - job_name: 'node_exporter'
     static_configs:
       - targets: ['localhost:9100']
   - job_name: 'nodes'
     metrics_path: /metrics    
     static_configs:
       - targets: ['localhost:5054']
   - job_name: 'validators'
     metrics_path: /metrics
     static_configs:
       - targets: ['localhost:5064']
EOF
```
{% endtab %}

{% tab title="Nimbus" %}
```bash
cat > $HOME/prometheus.yml << EOF
global:
  scrape_interval:     15s # By default, scrape targets every 15 seconds.

  # Attach these labels to any time series or alerts when communicating with
  # external systems (federation, remote storage, Alertmanager).
  external_labels:
    monitor: 'codelab-monitor'

# A scrape configuration containing exactly one endpoint to scrape:
# Here it's Prometheus itself.
scrape_configs:
   - job_name: 'node_exporter'
     static_configs:
       - targets: ['localhost:9100']
   - job_name: 'nodes'
     metrics_path: /metrics    
     static_configs:
       - targets: ['localhost:8008']
EOF
```
{% endtab %}

{% tab title="Teku" %}
```bash
cat > $HOME/prometheus.yml << EOF
global:
  scrape_interval:     15s # By default, scrape targets every 15 seconds.

  # Attach these labels to any time series or alerts when communicating with
  # external systems (federation, remote storage, Alertmanager).
  external_labels:
    monitor: 'codelab-monitor'

# A scrape configuration containing exactly one endpoint to scrape:
# Here it's Prometheus itself.
scrape_configs:
   - job_name: 'node_exporter'
     static_configs:
       - targets: ['localhost:9100']
   - job_name: 'nodes'
     metrics_path: /metrics    
     static_configs:
       - targets: ['localhost:8008']
EOF
```
{% endtab %}

{% tab title="Prysm" %}
```bash
cat > $HOME/prometheus.yml << EOF
global:
  scrape_interval:     15s # By default, scrape targets every 15 seconds.

  # Attach these labels to any time series or alerts when communicating with
  # external systems (federation, remote storage, Alertmanager).
  external_labels:
    monitor: 'codelab-monitor'

# A scrape configuration containing exactly one endpoint to scrape:
# Here it's Prometheus itself.
scrape_configs:
   - job_name: 'node_exporter'
     static_configs:
       - targets: ['localhost:9100']
   - job_name: 'validator'
     static_configs:
       - targets: ['localhost:8081']
   - job_name: 'beacon node'
     static_configs:
       - targets: ['localhost:8080']
   - job_name: 'slasher'
     static_configs:
       - targets: ['localhost:8082']
EOF
```
{% endtab %}

{% tab title="Lodestar" %}
```bash
cat > $HOME/prometheus.yml << EOF   
scrape_configs:
   - job_name: 'node_exporter'
     static_configs:
       - targets: ['localhost:9100']
   - job_name: 'Lodestar'
     metrics_path: /metrics    
     static_configs:
       - targets: ['localhost:8008']
EOF
```
{% endtab %}
{% endtabs %}

Configure prometheus para su nodo **eth1**. Empieza editando **prometheus.yml**

```bash
nano $HOME/prometheus.yml
```

Añade el fragmento de trabajo aplicable para tu nodo eth1 al final de **prometheus.yml**. Guardar el archivo.

{% tabs %}
{% tab title="Geth" %}
```bash
   - job_name: 'geth'
     scrape_interval: 15s
     scrape_timeout: 10s
     metrics_path: /debug/metrics/prometheus
     scheme: http
     static_configs:
     - targets: ['localhost:6060']
```
{% endtab %}

{% tab title="Besu" %}
```bash
   - job_name: 'besu'
     scrape_interval: 15s
     scrape_timeout: 10s
     metrics_path: /metrics
     scheme: http
     static_configs:
     - targets:
       - localhost:9545
```
{% endtab %}

{% tab title="Nethermind" %}
```bash
   - job_name: 'nethermind'
     scrape_interval: 15s
     scrape_timeout: 10s
     honor_labels: true
     static_configs:
       - targets: ['localhost:9091']
```

El monitoreo mental requiere [Prometheus Pushgateway](https://github.com/prometheus/pushgateway). Instalar con el siguiente comando.

```bash
sudo apt-get install -y prometheo's pushgateway
```

{% hint style="info" %}
Pushgateway escucha los datos de la mente en el puerto 9091.
{% endhint %}
{% endtab %}

{% tab title="OpenEthereum" %}
```bash
   - job_name: 'openethereum'
     scrape_interval: 15s
     scrape_timeout: 10s
     metrics_path: /metrics
     scheme: http
     static_configs:
     - targets: ['localhost:6060']
```
{% endtab %}
{% endtabs %}

Muévelo a `/etc/prometheus/prometheus.yml`

```bash
sudo mv $HOME/prometheus.yml /etc/prometheus/prometheus.yml
sudo chmod 644 /etc/prometheus/prometheus.yml
```

Por último, reinicie los servicios.

```bash
sudo systemctl restart grafana-server.service prometheus.service prometheus-node-exporter.service
```

Verificar que los servicios se están ejecutando correctamente:

```text
sudo systemctl status grafana-server.service prometheus.service prometheus-node-exporter.service
```

{% hint style="info" %}
💡 **Recordatorio**: Asegúrate de que el puerto 3000 esté abierto en el cortafuegos y/o el puerto reenviado si tienes la intención de ver la información de monitoreo desde una máquina diferente.
{% endhint %}

### 📶 6.2 Configurando Grafana Dashboards

1. Abre [http://localhost:3000](http://localhost:3000) o [http://&lt;your](http://<your) validator's ip address&gt;:3000 en tu navegador local.
2. Iniciar sesión con **admin** / **admin**
3. Cambiar contraseña
4. Haga clic en el icono **del equipo de configuración** , luego **Añadir fuente de datos**
5. Seleccione **Prometeo**
6. Establezca **Nombre** a **"Prometheus**"
7. Establecer **URL** a [http://localhost:9090](http://localhost:9090)
8. Haga clic en **Guardar & Prueba**
9. **Descargue y guarde** el archivo json de su Cliente ETH2. \[ [Lighthouse BC ](https://raw.githubusercontent.com/sigp/lighthouse-metrics/master/dashboards/Summary.json)\| [Lighthouse CV](https://raw.githubusercontent.com/sigp/lighthouse-metrics/master/dashboards/ValidatorClient.json) \| [Teku ](https://grafana.com/api/dashboards/13457/revisions/2/download)\| [Nimbus ](https://raw.githubusercontent.com/status-im/nimbus-eth2/master/grafana/beacon_nodes_Grafana_dashboard.json)\| [Prism ](https://raw.githubusercontent.com/GuillaumeMiralles/prysm-grafana-dashboard/master/less_10_validators.json)\| [Prisma &gt; 10 Validadores](https://raw.githubusercontent.com/GuillaumeMiralles/prysm-grafana-dashboard/master/more_10_validators.json) \| Lodestar \]
10. **Descargue y guarde** el archivo json de su cliente ETH1 \[ [Geth](https://gist.githubusercontent.com/karalabe/e7ca79abdec54755ceae09c08bd090cd/raw/3a400ab90f9402f2233280afd086cb9d6aac2111/dashboard.json) \| [Besu ](https://grafana.com/api/dashboards/10273/revisions/5/download)\| [Nethermind ](https://raw.githubusercontent.com/NethermindEth/metrics-infrastructure/master/grafana/dashboards/nethermind.json)\| [OpenEthereum ](https://raw.githubusercontent.com/dappnode/DAppNodePackage-openethereum/master/openethereum-grafana-dashboard.json)\]
11. Haga clic en **Crear +** icono &gt; **Importar**
12. Añadir el panel de control del cliente ETH2 a través de **Subir archivo JSON**
13. Si es necesario, seleccione Prometheus como **Data Source**.
14. Haga clic en el botón **Importar**
15. Repita los pasos 11-14 para el panel de control del cliente ETH1.

{% hint style="info" %}
🔥 **Resolución de problemas comunes de Grafana**:

_Los paneles no muestran datos de nodos eth1._

* En el archivo de unidad eth1 _\*\*_ bajo ubicado en `/etc/systemd/system/eth1. ervice`, asegúrese de que su nodo/geth eth1 se inicie con los parámetros correctos, de modo que las métricas de informe y el servidor http pprof estén habilitados.
  * Example:`ExecStartPre = /usr/bin/geth --http --metrics --pprof`
{% endhint %}

#### Ejemplo de tableros Grafana para cada cliente ETH2.

{% tabs %}
{% tab title="Lighthouse" %}
![](../../.gitbook/assets/lighthouse-validator.png)

![](../../.gitbook/assets/lhm.png)

Créditos: [https://github.com/sigp/lighthouse-metrics/](https://github.com/sigp/lighthouse-metrics/)
{% endtab %}

{% tab title="Nimbus" %}
![](../../.gitbook/assets/nim_dashboard.png)

Créditos: [https://github.com/status-im/nimbus-eth2/](https://github.com/status-im/nimbus-eth2/)
{% endtab %}

{% tab title="Teku" %}
![](../../.gitbook/assets/teku.dash.png)

Créditos: [https://grafana.com/grafana/dashboards/13457](https://grafana.com/grafana/dashboards/13457)
{% endtab %}

{% tab title="Prysm" %}
![](../../.gitbook/assets/prysm_dash.png)

Créditos: [https://github.com/GuillaumeMiralles/prysm-grafana-dashboard](https://github.com/GuillaumeMiralles/prysm-grafana-dashboard)
{% endtab %}

{% tab title="Lodestar" %}
Trabajos en curso.
{% endtab %}
{% endtabs %}

#### Ejemplo de paneles de Grafana para cada nodo ETH1.

{% tabs %}
{% tab title="Geth" %}
![](../../.gitbook/assets/geth-dash.png)

Créditos: [https://gist.github.com/karalabe/e7ca79abdec54755ceae09c08bd090cd](https://gist.github.com/karalabe/e7ca79abdec54755ceae09c08bd090cd)
{% endtab %}

{% tab title="Besu" %}
![](../../.gitbook/assets/besu-dash.png)

Créditos: [https://grafana.com/dashboards/10273](https://grafana.com/dashboards/10273)
{% endtab %}

{% tab title="Nethermind" %}
![](../../.gitbook/assets/nethermind-dash.png)

Créditos: [https://github.com/\)\[video\] mindEth/metrics-infrastructure](https://github.com/NethermindEth/metrics-infrastructure)
{% endtab %}

{% tab title="OpenEthereum" %}
![](../../.gitbook/assets/openethereum-dashboard.png)
{% endtab %}
{% endtabs %}

### ⚠ 6.3 Configurar notificaciones de alerta

{% hint style="info" %}
Configurar alertas para recibir notificaciones si sus validadores se quedan sin conexión.
{% endhint %}

Recibe notificaciones de problemas con tus validadores. Elija entre correo electrónico, telegram, discord o slack.

{% tabs %}
{% tab title="Email Notifications" %}
1. Visita [https://beaconcha.in/](https://beaconcha.in/)
2. Regístrate en una cuenta.
3. Verifique su **correo electrónico**
4. Busca la dirección pública de tu validador _\*\*_
5. Añade validadores a tu lista de seguimiento haciendo clic en el **símbolo del marcador**.
{% endtab %}

{% tab title="Telegram Notifications" %}
1. En el menú de Grafana, seleccione **Canales de notificación** debajo del icono de la campana.
2. Haga clic en **Añadir canal**.
3. Dale al canal de notificación un **nombre**.
4. Seleccione **Telegram** de la lista Tipos.
5. Para completar la **configuración de la API de Telegram**, se requiere un **canal de Telegram** y **bot**. Para instrucciones sobre cómo configurar un bot con `@Botfather`, vea [esta sección](https://core.telegram.org/bots#6-botfather) de la documentación de Telegram. Necesitas crear un token de la API BOT.
6. Crear un nuevo grupo de telegramas.
7. Invita al bot a tu nuevo grupo.
8. Escriba al menos 1 mensaje en el grupo para inicializarlo.
9. Visit [`https://api.telegram.org/botXXX:YYY/getUpdates`](https://api.telegram.org/botXXX:YYY/getUpdates) where `XXX:YYY` is your BOT API Token.
10. En la respuesta JSON, encuentra y copia el **Chat ID**. Encuéntralo entre **chat** y **título**. _Ejemplo de ID de Chat_: `-1123123123`

    ```text
    "chat":{"id":-123123123,"title":
    ```

11. Pegue el **Chat ID** en el campo correspondiente en **Grafana**.
12. **Guarda y prueba** el canal de notificaciones para tus alertas.
13. Ahora puede crear alertas personalizadas desde sus paneles. [Visita aquí para aprender a crear alertas.](https://grafana.com/docs/grafana/latest/alerting/create-alerts/)
{% endtab %}

{% tab title="Discord Notifications" %}
1. En el menú de Grafana, seleccione **Canales de notificación** debajo del icono de la campana.
2. Haga clic en **Añadir canal**.
3. Añade un **nombre** al canal de notificación.
4. Selecciona **Discord** de la lista de tipos.
5. Para completar la configuración, se requiere un servidor de Discord \(y un canal de texto disponible\) así como una URL de Webhook. Para obtener instrucciones sobre cómo configurar un Webhook de Discord, consulte [esta sección](https://support.discord.com/hc/en-us/articles/228383668-Intro-to-Webhooks) de su documentación.
6. Introduzca el Webhook **URL** en el panel de configuración de notificación de Discord.
7. Haz clic en **Enviar prueba**, que enviará un mensaje de confirmación al canal de Discord.
{% endtab %}

{% tab title="Slack Notifications" %}
1. En el menú de Grafana, seleccione **Canales de notificación** debajo del icono de la campana.
2. Haga clic en **Añadir canal**.
3. Añade un **nombre** al canal de notificación.
4. Selecciona **Slack** de la lista Tipos.
5. Para obtener instrucciones sobre cómo configurar un webhook entrante de Slack, consulte [esta sección](https://api.slack.com/messaging/webhooks) de su documentación.
6. Introduzca la URL de Slack Incoming Webhook en el campo **URL**.
7. Haga clic en **Enviar prueba**, que enviará un mensaje de confirmación al canal de Slack.
{% endtab %}
{% endtabs %}

### 🌊 6.4 Monitoreo con Comprobación de Tiempo Actualizado por Google Cloud

{% hint style="info" %}
¿Quién vigila el vigilante? Con una herramienta externa de terceros como Uptime Check, puede tener mayores garantías de que su validador está funcionando en caso de desastres como fallo de energía, fallo de hardware o interrupción de Internet. En estos escenarios, la supervisión mencionada anteriormente por Prometeo y Grafana probablemente dejaría de funcionar también.

Créditos a [Mohamed Mansour por inspirar esta guía](https://www.youtube.com/watch?v=txgOVDTemPQ).
{% endhint %}

He aquí cómo configurar un servicio de monitorización sin coste llamado Uptime Check por Google.

{% hint style="info" %}
Para una demostración de vídeo, ve [vídeos educativos de MohamedMansour's eth2](https://www.youtube.com/watch?v=txgOVDTemPQ). Por favor, apoya su concesión [GITCOIN](https://gitcoin.co/grants/1709/video-educational-grant). 🙏
{% endhint %}

1. Visita [cloud.google.com](https://cloud.google.com/)
2. Buscar **Monitorización** en el campo de búsqueda.
3. Haga clic en **Seleccionar un proyecto para empezar a monitorizar**.
4. Haga clic en **Nuevo proyecto**
5. **Nombre** su proyecto y haga clic en **Crear.**
6. En el menú de notificaciones, seleccione su nuevo proyecto.
7. En la columna de la derecha, hay una Tarjeta de Vigilancia. Haga clic en **Ir al seguimiento**.
8. En el menú de la izquierda, haga clic en **Comprobaciones de tiempo de actualización** y luego **CHELIAR CHECK.**
9. Escriba un título, p.e. _**Nodo Geth**_
10. Seleccionar protocolo como _**TCP**_
11. Introduzca su dirección IP pública y número de puerto. es decir, ip=**7.55.6.3** y puerto =**30303**
12. Seleccione la frecuencia deseada para comprobar, por ejemplo, **5 minutos**
13. Elija la región más cercana a usted para comprobar. Haga clic a continuación.
14. Crear un canal de notificación. Haga clic en **Administrar canales de notificación.**
15. Elija la configuración deseada. Elegir de cualquiera o de todos Slack, Webhook, Email o SMS.
16. Volver a Crear ventana de Comprobar Uptime.
17. Dentro del campo de notificaciones, haz clic en el botón de actualizar para cargar tus nuevos canales de notificación.
18. Seleccione las notificaciones deseadas.
19. Haga clic en **TEST** para verificar que las notificaciones están configuradas correctamente.
20. Haga clic en **CREATE** para terminar.

{% hint style="success" %}
🎉¡Felicidades por configurar tu validador! Es bueno ir a eth2.0.

¿Encontraste útil nuestra guía? Háganos saber con un consejo y seguiremos actualizándolo.

Usa [cointr.ee para encontrar nuestras direcciones de donación ](https://cointr.ee/coincashew). 🙏

Cualquier comentario y todas las solicitudes de extracción son muy apreciadas. 🌛

Descubra y chatee con otros interesados en Discord @

[https://discord.gg/w8Bx8W2HPW](https://discord.gg/w8Bx8W2HPW)😃
{% endhint %}

## 🧙7. Actualizar una cliente ETH2

Cuando se corta una nueva versión, querrá actualizar a la última versión estable. A continuación le muestra cómo actualizar su cadena de baliza eth2 y validador.

{% hint style="info" %}
Revise siempre los registros de **git con el comando`git log`** o **las notas de lanzamiento** antes de actualizar. Puede haber cambios que requieran su atención.
{% endhint %}

Seleccione su cliente ETH2.

{% tabs %}
{% tab title="Lighthouse" %}
Revise las notas de la versión y compruebe si se rompen cambios/características.

[https://github.com/sigp/lighthouse/releases](https://github.com/sigp/lighthouse/releases)

Desplegar el último código fuente y construirlo.

```bash
cd $HOME/git/lighthouse
git fetch --all && git checkout stable && git pull
make
```

Verifique la versión completada comprobando el número de la nueva versión.

```bash
lighthouse --version
```

Reinicie la cadena de baliza y el validador según los procedimientos operativos normales.

```text
sudo systemctl reload-or-restart beacon-chain validator
```
{% endtab %}

{% tab title="Nimbus" %}
Revise las notas de la versión y compruebe si se rompen cambios/características.

[https://github.com/status-im/nimbus-eth2/releases](https://github.com/status-im/nimbus-eth2/releases)

Desplegar el último código fuente y construirlo.

```bash
cd $HOME/git/nimbus-eth2
git pull && make update
make NIMFLAGS="-d:insecure" nimbus_beacon_node
```

Verifique la versión completada comprobando el número de la nueva versión.

```bash
cd $HOME/git/nimbus-eth2/build
./nimbus_beacon_node --version
```

Detiene, copie el nuevo binario y reinicie la cadena de baliza y el validador según los procedimientos operativos normales.

```bash
sudo systemctl stop beacon-chain
sudo rm /usr/bin/nimbus_beacon_node
sudo cp $HOME/git/nimbus-eth2/build/nimbus_beacon_node /usr/bin
sudo systemctl reload-or-restart beacon-chain
```
{% endtab %}

{% tab title="Teku" %}
Revise las notas de la versión y compruebe si se rompen cambios/características.

[https://github.com/ConsenSys/teku/releases](https://github.com/ConsenSys/teku/releases)

Desplegar el último código fuente y construirlo.

```bash
cd $HOME/git/teku
git pull
./gradlew distTar installDist
```

Verifique la versión completada comprobando el número de la nueva versión.

```bash
cd $HOME/git/teku/build/install/teku/bin
./teku --version
```

Reinicie la cadena de baliza y el validador según los procedimientos operativos normales.

```bash
sudo systemctl stop beacon-chain
sudo rm -rf /usr/bin/teku
sudo cp -r $HOME/git/teku/build/install/teku /usr/bin/teku
sudo systemctl reload-or-restart beacon-chain
```
{% endtab %}

{% tab title="Prysm" %}
Revise las notas de la versión y compruebe si se rompen cambios/características. [https://github.com/prysmaticlabs/prysm/releases](https://github.com/prysmaticlabs/prysm/releases)

```bash
#Simplemente reinicie los procesos
sudo systemctl reload-or-restart beacon-chain validator
```
{% endtab %}

{% tab title="Lodestar" %}
Revise las notas de la versión y compruebe si se rompen cambios/características.

[https://github.com/ChainSafe/lodestar/releases](https://github.com/ChainSafe/lodestar/releases)

Desplegar el último código fuente y construirlo.

```bash
cd $HOME/git/lodestar
git pull
yarn install --ignore-optional
yarn run build
```

Verifique la versión completada comprobando el número de la nueva versión.

```bash
./lodestar --version
```

Reinicie la cadena de baliza y el validador según los procedimientos operativos normales.

```text
sudo systemctl reload-or-restart beacon-chain validator
```
{% endtab %}
{% endtabs %}

Marque los registros para verificar que los servicios están funcionando correctamente y asegurarse de que no hay errores.

{% tabs %}
{% tab title="Faro \| Prisma \| Lodestar" %}
```bash
sudo systemctl status beacon-chain validator
```
{% endtab %}

{% tab title="Nimbus \| Teku" %}
```text
sudo systemctl status beacon-chain
```
{% endtab %}
{% endtabs %}

## 🔥8. Consejos útiles adicionales

### 🛑 8.1 Salir voluntariamente de un validador

{% hint style="info" %}
Utiliza este comando para indicar tus intenciones de dejar de validar con tu validador. Esto significa que ya no quieres apostar con tu validador y quieres apagar tu nodo.

* La salida voluntaria toma un mínimo de 2048 epochs \(o ~9días\). Hay una cola para salir y un retraso antes de que el validador se cierre por fin.
* Una vez que un validador haya terminado en la fase 0, esto no es revertible y ya no puede volver a validar de nuevo.
* Sus fondos no estarán disponibles para su retiro hasta la fase 1.5 o posterior.
* Después de que su validador salga de la cola de salida y esté realmente cerrado, es seguro apagar su nodo y validador.
{% endhint %}

{% tabs %}
{% tab title="Lighthouse" %}
```bash
lighthouse account validator exit \
--keystore $HOME/.lighthouse/mainnet/validators \
--beacon-node http://localhost:5052 \
--network mainnet
```
{% endtab %}

{% tab title="Teku" %}
```bash
teku voluntary-exit \
--epoch=<epoch number to exit> \
--beacon-node-api-endpoint=http://127.0.0.1:5051 \
--validator-keys=<path to keystore.json>:<path to password.txt file>
```
{% endtab %}

{% tab title="Nimbus" %}
```bash
build/nimbus_beacon_node deposits exit --validator=<VALIDATOR_PUBLIC_KEY> --data-dir=/var/lib/nimbus
```
{% endtab %}

{% tab title="Prysm" %}
```bash
$HOME/prysm/prysm.sh validator accounts voluntary-exit
```
{% endtab %}

{% tab title="Lodestar" %}
```bash
./lodestar account validator voluntary-exit --publicKey 0xF00
```
{% endtab %}
{% endtabs %}

### 🗝 8.2 Verifique su frase mnemónica

Utilizando la herramienta eth2deposit-cli, asegúrese de que puede regenerar los mismos pares de claves eth2 restaurando sus `validator_keys`

```bash
cd $HOME/eth2deposit-cli 
./deposit.sh existing-mnemonic --chain mainnet
```

{% hint style="info" %}
Cuando la **pubkey** en ambos **archivos del almacén de claves** son **idénticos,** esto significa que su frase mnemónica es veritativamente correcta. Otros campos serán diferentes debido a la salazón.
{% endhint %}

### 🤖8.3 Añadir validadores adicionales

Usando la herramienta eth2deposit-cli, puede agregar más validadores creando un nuevo archivo de datos de depósito y `validator_keys`

Primero, copia de seguridad y mueve el directorio `validator_key` existente y añade la fecha al final.

```bash
cd $HOME/eth2deposit-cli
mv validator_key validator_key_$(date +"%Y%d%m-%H%M%S")
```

Por ejemplo, en caso de que originalmente creamos 3 validadores pero ahora queremos añadir 5 validadores más, podríamos usar el siguiente comando.

```bash
cd $HOME/eth2deposit-cli
./deposit.sh existing-mnemonic --validator_start_index 3 --num_validators 5 --chain mainnet
```

Completa los pasos para subir el `deposit_data-#########.json` al sitio del panel de lanzamiento y realiza tus 32 transacciones de depósito ETH correspondientes.

Termina deteniendo el validador, importando la nueva clave del validador\(s\), reiniciando el validador y verificando los registros asegurándose de que todo funcione sin error.

### 💸 8.4 Cambiar/migrar clientes Eth2 con protección antibarra

{% hint style="info" %}
La clave de despegue en este proceso es evitar ejecutar dos clientes eth2 simultáneamente. Quieren evitar que se les castigue con un castigo de rebano, que causa una pérdida de éter.
{% endhint %}

#### 🛑 8.4.1 Detener la vieja cadena de baliza y el validador antiguo.

Para exportar la base de datos de barras, es necesario detener el validador.

{% tabs %}
{% tab title="Faro \| Prisma \| Lodestar" %}
```bash
sudo systemctl stop beacon-chain validator
```
{% endtab %}

{% tab title="Nimbus \| Teku" %}
```text
sudo systemctl stop beacon-chain
```
{% endtab %}
{% endtabs %}

#### 💽 8.4.2 Exportar base de datos de barras \[Opcional\]

{% hint style="info" %}
[EIP-3076](https://eips.ethereum.org/EIPS/eip-3076) implementa un estándar para la seguridad migrar claves validadoras entre clientes eth2. Este es el contenido exportado de la base de datos de barras.
{% endhint %}

Actualizar la ubicación y el nombre del archivo exportado .json.

{% tabs %}
{% tab title="Lighthouse" %}
```bash
lighthouse account validator slashing-protection export <lighthouse_interchange.json>
```
{% endtab %}

{% tab title="Nimbus" %}
A implementar
{% endtab %}

{% tab title="Teku" %}
```bash
teku slashing-protection export --to=<FILE>
```
{% endtab %}

{% tab title="Prysm" %}
```bash
prysm.sh validator slashing-protection export --datadir=/path/to/your/wallet --slashing-protection-export-dir=/path/to/desired/outputdir
```
{% endtab %}

{% tab title="Lodestar" %}
```bash
./lodestar account validator slashing-protection export --network mainnet --file interchange.json
```
{% endtab %}
{% endtabs %}

#### 🚧 8.4.3 Configurar e instalar una nueva cadena validadora / baliza

Ahora necesita configurar/instalar su nuevo validador **pero no empezar a ejecutar los procesos del sistema**. Be sure to thoroughly follow your new validator's [Section 4. Configure una cadena y validador de baliza ETH2.](guide-or-how-to-setup-a-validator-on-eth2-testnet.md#4-configure-a-eth2-beacon-chain-node-and-validator) Necesitará construir/instalar el cliente, configurar el reenvío de puertos/firewalls, y nuevos archivos de unidades del sistema.

{% hint style="warning" %}
✨ **Consejo Pro**: Durante el proceso de reimportación de claves validadoras, **espera por lo menos 13 minutos** o dos epoches para evitar que se corte penalidades. Debe evitar ejecutar dos clientes eth2 con las mismas claves de validador al mismo tiempo.
{% endhint %}

{% hint style="danger" %}
🛑 **Paso crítico**: No inicie ningún **proceso de sistema** hasta que haya **importado la base de datos slashing** o haya **esperado al menos 13 minutos o dos epochs**.
{% endhint %}

#### 📂 8.4.4 Importar base de datos de barrido \\(Opcional\\)

Usando su nuevo cliente eth2, ejecute el siguiente comando y actualice la ruta relevante para importar su base de datos de barras desde hace 2 pasos.

{% tabs %}
{% tab title="Lighthouse" %}
```bash
lighthouse account validator slashing-protection import <my_interchange.json>
```
{% endtab %}

{% tab title="Nimbus" %}
A implementar
{% endtab %}

{% tab title="Teku" %}
```bash
teku slashing-protection import --from=<FILE>
```
{% endtab %}

{% tab title="Prysm" %}
```bash
prysm.sh validator slashing-protection import --datadir=/path/to/your/wallet --slashing-protection-json-file=/path/to/desiredimportfile
```
{% endtab %}

{% tab title="Lodestar" %}
```bash
prysm.sh validator slashing-protection import --datadir=/path/to/your/wallet --slashing-protection-json-file=/path/to/desiredimportfile
```
{% endtab %}
{% endtabs %}

#### 🌠 8.4.5 Iniciar nuevo validador y nueva cadena de baliza

{% tabs %}
{% tab title="Faro \| Prisma \| Lodestar" %}
```bash
sudo systemctl start beacon-chain validator
```
{% endtab %}

{% tab title="Nimbus \| Teku" %}
```text
sudo systemctl start beacon-chain
```
{% endtab %}
{% endtabs %}

#### 🔥 8.4.6 Verificar funcionalidad

Marque los registros para verificar que los servicios están funcionando correctamente y asegurarse de que no hay errores.

{% tabs %}
{% tab title="Faro \| Prisma \| Lodestar" %}
```bash
sudo systemctl status beacon-chain validator
```
{% endtab %}

{% tab title="Nimbus \| Teku" %}
```text
sudo systemctl status beacon-chain
```
{% endtab %}
{% endtabs %}

Finalmente, verifique que los certificados de su validador están trabajando con el explorador de bloques público como

[https://beaconcha.in/](https://beaconcha.in/)

Introduzca la pubkey de su validador para ver su estado.

#### 🧯 Seguimiento de Actualización 8.4.7 con Prometheus y Grafana

[Revise la sección 6](guide-or-how-to-setup-a-validator-on-eth2-testnet.md#6-monitoring-your-validator-with-grafana-and-prometheus) y cambie su `prometheus.yml`. Asegúrese de que prometheus está conectado al nuevo puerto de métricas de su cliente eth2. También querrá importar el panel de control de su nuevo cliente eth2.

### 🖥 8.5 Usar todo el espacio disponible en disco LVM

Durante la instalación del Servidor Ubuntu, surge un problema común donde el espacio de su disco duro no está completamente disponible para su uso.

```bash
# Ver las unidades de disco
sudo -s lvm

# Cambiar la ruta del sistema de archivos de volumen lógico si es necesario
lvextend -l +100%F/etc/dev/ubuntu-vg/ubuntu-lv

#exit lvextend
exit

# Redimensionar el sistema de archivos para usar el nuevo espacio disponible en el volumen lógico
resize2fs /dev/ubuntu-vg/ubuntu-lv

## Verificar el nuevo espacio disponible
df -h
```

**Referencia de origen**: [https://askubuntu.com/questions/1106795/ubuntu-server-18-04-lvm-out-of-space-with-improper-default-partitioning](https://askubuntu.com/questions/1106795/ubuntu-server-18-04-lvm-out-of-space-with-improper-default-partitioning)

### 8.6 Reducir el uso del ancho de banda de la red

{% hint style="info" %}
Alojando su propio nodo ETH1 puede consumir cientos de gigabytes de datos por día. Debido a que los planes de datos pueden ser limitados o costosos, puede desear ralentizar el uso de datos pero mantener una buena conectividad a la red.
{% endhint %}

Edite su archivo de unidad de servicio eth1.service .

```bash
sudo nano /etc/systemd/system/eth1.service
```

Añade la siguiente bandera para limitar el número de pares en la línea `ExecStart`.

{% tabs %}
{% tab title="Geth" %}
```bash
--maxpeers 10
# Ejemplo
# ExecStart       = /usr/bin/geth --maxpeers 10 --http --ws
```
{% endtab %}

{% tab title="OpenEthereum \(Paridad\)" %}
```bash
--max-peers 10
# Ejemplo
# ExecStart       = <home directory>/openethereum/openethereum --max-peers 10
```
{% endtab %}

{% tab title="Besu" %}
```bash
--max-peers 10
# Ejemplo
# ExecStart = <home directory>/besu/bin/besu --max-peers 10 --rpc-http-enabled
```
{% endtab %}

{% tab title="Nethermind" %}
```bash
--Network.ActivePeersMaxCount 10
# Ejemplo 
 # ExecStart       = <home directory>/nethermind/Nethermind.Runner --Network.ActivePeersMaxCount 10 --JsonRpc.Enabled true
```
{% endtab %}
{% endtabs %}

Por último, vuelva a cargar el nuevo archivo de unidad y reinicie el nodo eth1.

```bash
sudo systemctl daemon-reload
sudo systemctl restart eth1
```

### 📂 8.7 Ubicaciones de directorios importantes

{% hint style="info" %}
En caso de que necesite localizar sus claves de validador, directorios de base de datos u otros archivos importantes.
{% endhint %}

#### Archivos y ubicaciones del cliente Eth2

{% tabs %}
{% tab title="Lighthouse" %}
```bash
# Llaves de validador
~/.lighthouse/mainnet/validators

# Datos de cadena de baliza
~/.lighthouse/mainnet/beacon

# Lista de todos los validadores y contraseñas
~/.lighthouse/mainnet/validators/validator_definitions.yml

#Db de protección de barra slash
~/.lighthouse/mainnet/validators/slashing_protection.sqlite
```
{% endtab %}

{% tab title="Nimbus" %}
```bash
# Claves del validador
/var/lib/nimbus/validators

# Función de datos
/var/lib/nimbus/db

#Protección de Slash db
/var/lib/nimbus/validators/slashing_protection.sqlite3

#Registrs
/var/lib/nimbus/beacon.log
```
{% endtab %}

{% tab title="Teku" %}
```bash
# Claves del validador
/var/lib/teku

# Datos de la cadena del Beacon
~/tekudata/beacon

#Protección de Slash db
~/tekudata/validator/slashprotection
```
{% endtab %}

{% tab title="Prysm" %}
```bash
# Llaves del validador
~/.eth2validators/prysm-wallet-v2/direct

# Datos de cadena del faro
~/.eth2/beaconchaindata
```
{% endtab %}

{% tab title="Lodestar" %}
```bash
# Llaves del validador
$rootDir/keystores

# Validator Secrets
$rootDir/secrets

# Validator DB Data
$rootDir/validator-db
```
{% endtab %}
{% endtabs %}

#### Archivos y ubicaciones de nodos Eth1

{% tabs %}
{% tab title="Geth" %}
```bash
# ubicación de base de datos
$HOME/.ethereum
```
{% endtab %}

{% tab title="OpenEthereum \(Paridad\)" %}
```bash
# ubicación de base de datos
$HOME/.local/share/openethereum
```
{% endtab %}

{% tab title="Besu" %}
```bash
# ubicación de base de datos
$HOME/.besu/database
```
{% endtab %}

{% tab title="Nethermind" %}
```bash
#ubicación de base de datos
$HOME/.nethermind/nethermind_db/mainnet
```
{% endtab %}
{% endtabs %}

### 8.8 Hosting ETH1 nodo en una máquina diferente

{% hint style="info" %}
Alojando su propio nodo ETH1 en una máquina diferente de donde residen su cadena de baliza y validador, puede permitir cierta modularidad y flexibilidad extra.
{% endhint %}

En la máquina de nodos eth1, edite su archivo de unidad eth1.service.

```bash
sudo nano /etc/systemd/system/eth1.service
```

Agregue la siguiente bandera para permitir el http entrante remoto o solicitudes api websocket en la línea `ExecStart`.

{% hint style="info" %}
Si no se usan websockets, no es necesario incluir los parámetros ws. Sólo Nimbus requiere websockets.
{% endhint %}

{% tabs %}
{% tab title="Geth" %}
```bash
--http.addr 0.0.0.0 --ws.addr 0.0.0.0
# Ejemplo
# ExecStart       = /usr/bin/geth --http.addr 0.0.0.0 --ws.addr 0.0.0.0 --http --ws
```
{% endtab %}

{% tab title="OpenEthereum \(Paridad\)" %}
```bash
--jsonrpc-interface=all --ws-interface=all
# Ejemplo 
# Ejemplo = <home directory>/openethereum/openethereum --jsonrpc-interface=all --ws-interface=all
```
{% endtab %}

{% tab title="Besu" %}
```bash
--rpc-http-host=0.0.0 --rpc-ws-enabled --rpc-ws-host=0.0.0
# Ejemplo 
 # ExecStart = <home directory>/besu/bin/besu --rpc-http-host=0.0.0 --rpc-ws-enabled --rpc-ws-host=0.0.0.0 --rpc-http-enabled
```
{% endtab %}

{% tab title="Nethermind" %}
```bash
--JsonRpc.Host 0.0.0 --WebSocketsActivado
# Ejemplo 
# ExecStart       = <home directory>/nethermind/Nethermind.Runner --JsonRpc.Host 0.0.0.0 --WebSocketsEnabled --JsonRpc.Enabled true 
```
{% endtab %}
{% endtabs %}

Recarga el nuevo archivo de unidad y reinicia el nodo eth1.

```bash
sudo systemctl daemon-reload
sudo systemctl restart eth1
```

En la máquina separada que aloja la cadena beacon-chain, actualice el archivo de unidad beacon-chain con la dirección IP del nodo eth1.

{% tabs %}
{% tab title="Lighthouse" %}
```bash
# edit beacon-chain unit file
nano /etc/systemd/system/beacon-chain.service
# add the --eth1-endpoints parameter
# Ejemplos
# --eth1-endpoints=http://192.168.10.22
```
{% endtab %}

{% tab title="Nimbus" %}
```bash
# edit beacon chain unit file
nano /etc/systemd/system/beacon-chain.service
# modify the --web-url parameter
# Ejemplos
# --web3-url=ws://192.168.10.22
```
{% endtab %}

{% tab title="Teku" %}
```bash
# edit teku.yaml
nano /etc/teku/teku.yaml
# cambia el eth1-endpoint
# Ejemplos
# eth1-endpoint: "http://192.168.10.20:8545"
```
{% endtab %}

{% tab title="Prysm" %}
```bash
# edit beacon-chain unit file
nano /etc/systemd/system/beacon-chain.service
# add the --http-web3provider parameter
# Ejemplos
# --http-web3provider=http://192.168.10.20:8545
```
{% endtab %}

{% tab title="Lodestar" %}
```bash
# edit beacon-chain unit file
nano /etc/systemd/system/beacon-chain.service
# add the --eth1.providerUrl parameter
# Ejemplos
# --eth1.providerUrl http://192.168.10.20:8545
```
{% endtab %}
{% endtabs %}

Recarga el archivo de unidad actualizado y reinicia la cadena beacon-chain.

```bash
sudo systemctl daemon-reload
sudo systemctl restart beacon-chain
```

### 🎊 8.9 Añadir o cambiar la bandera graffiti POAP

Configure su `graffiti`, un mensaje personalizado incluido en los bloques que su validador proponga con éxito, y gane un token POAP de validador de cadena de baliza temprano. [Genera tu cadena POAP suministrando una dirección de Ethereum 1.0 aquí.](https://beaconcha.in/poap)

Ejecute el siguiente comando para establecer la variable `MY_GRAFFITI`. Reemplazar `<my POAP string or message>` entre las comillas simples.

```bash
MY_GRAFFITI='<my POAP string or message>'
# Ejemplos
# MY_GRAFFITI='poapAAAAACGatUA1bLuDnL4FMD13BfoD'
# MY_GRAFFITI='eth2 rulez!'
```

{% hint style="info" %}
Aprende más sobre [POAP - La ficha de prueba de asistencia. ](https://www.poap.xyz/)
{% endhint %}

{% tabs %}
{% tab title="Lighthouse" %}
Ejecute lo siguiente para volver a crear un **archivo de unidad** para definir la configuración de su`validator.service`. Simplemente copie y pegue.

```bash
cat > $HOME/validator.service << EOF 
# The eth2 validator service (part of systemd)
# file: /etc/systemd/system/validator.service 

[Unit]
Description     = eth2 validator service
Wants           = network-online.target beacon-chain.service
After           = network-online.target 

[Service]
User            = $(whoami)
ExecStart       = $(which lighthouse) vc --network mainnet --graffiti "${MY_GRAFFITI}" 
Restart         = on-failure

[Install]
WantedBy    = multi-user.target
EOF
```

Mover el archivo de unidad a `/etc/systemd/system`

```bash
sudo mv $HOME/validator.service /etc/systemd/system/validator.service
```

Actualizar permisos de archivo.

```bash
sudo chmod 644 /etc/systemd/system/validator.service
```
{% endtab %}

{% tab title="Nimbus" %}
Ejecute lo siguiente para volver a crear un **archivo de unidad** para definir su configuración`beacon-chain.service`. Simplemente copie y pegue.

```bash
cat > $HOME/beacon-chain.service << EOF 
# The eth2 beacon chain service (part of systemd)
# file: /etc/systemd/system/beacon-chain.service 

[Unit]
Description     = eth2 beacon chain service
Wants           = network-online.target
After           = network-online.target 

[Service]
Type            = simple
User            = $(whoami)
WorkingDirectory= /var/lib/nimbus
ExecStart       = /usr/bin/nimbus_beacon_node --network=mainnet --graffiti="${MY_GRAFFITI}" --data-dir=/var/lib/nimbus --web3-url=ws://127.0.0.1:8546 --metrics --metrics-port=8008 --rpc --rpc-port=9091 --validators-dir=/var/lib/nimbus/validators --secrets-dir=/var/lib/nimbus/secrets --log-file=/var/lib/nimbus/beacon.log
Restart         = on-failure

[Install]
WantedBy    = multi-user.target
EOF
```

{% hint style="warning" %}
Nimbus sólo soporta conexiones websocket \("ws://" y "wss://"\) para el nodo ETH1. Geth, OpenEthereum, Infura and Chainstack ETH1 nodes are verified compatible.
{% endhint %}

Mover el archivo de unidad a `p/systemd/system`

```bash
sudo mv $HOME/beacon-chain.service /etc/systemd/system/beacon-chain.service
```

Actualizar permisos de archivo.

```bash
sudo chmod 644 c/systemd/beacon-chain.service
```
{% endtab %}

{% tab title="Teku" %}
Vuelva a generar su archivo de configuración Teku. Simplemente copie y pegue.

```bash
cat > $HOME/teku.yaml << EOF
# network
network: "mainnet"

# p2p
p2p-enabled: true
p2p-port: 9000
# validators
validator-keys: "/var/lib/teku/validator_keys:/var/lib/teku/validator_keys"
validators-graffiti: "${MY_GRAFFITI}"

# Eth 1
eth1-endpoint: "http://localhost:8545"

# metrics
metrics-enabled: true
metrics-categories: ["BEACON","LIBP2P","NETWORK"]
metrics-port: 8008

# database
data-path: "$(echo $HOME)/tekudata"
data-storage-mode: "archive"

# rest api
rest-api-port: 5051
rest-api-docs-enabled: true
rest-api-enabled: true

# logging
log-include-validator-duties-enabled: true
log-destination: CONSOLE
EOF
```

Mover el archivo de configuración a `mañ/teku`

```bash
sudo mv $HOME/teku.yaml /teku/teku.yaml
```
{% endtab %}

{% tab title="Prysm" %}
Re-crear un **archivo de unidad** para definir la configuración de su`validator.service`. Simplemente copie y pegue.

```bash
cat > $HOME/validator.service << EOF 
# The eth2 validator service (part of systemd)
# file: /etc/systemd/system/validator.service 

[Unit]
Description     = eth2 validator service
Wants           = network-online.target beacon-chain.service
After           = network-online.target 

[Service]
User            = $(whoami)
ExecStart       = $(echo $HOME)/prysm/prysm.sh validator --mainnet --graffiti "${MY_GRAFFITI}" --accept-terms-of-use --wallet-password-file $(echo $HOME)/.eth2validators/validators-password.txt
Restart         = on-failure

[Install]
WantedBy	= multi-user.target
EOF
```

Mover el archivo de unidad a `p/systemd/system`

```bash
sudo mv $HOME/validator.service /etc/systemd/system/validator.service
```

Actualizar sus permisos.

```bash
sudo chmod 644 c/systemd/validator.service
```
{% endtab %}

{% tab title="Lodestar" %}
Ejecute lo siguiente para volver a crear un **archivo de unidad** para definir la configuración de su`validator.service`. Simplemente copie y pegue.

```bash
cat > $HOME/validator.service << EOF 
# The eth2 validator service (part of systemd)
# file: /etc/systemd/system/validator.service 

[Unit]
Description     = eth2 validator service
Wants           = network-online.target beacon-chain.service
After           = network-online.target 

[Service]
User            = $(whoami)
WorkingDirectory= $(echo $HOME)/git/lodestar
ExecStart       = $(echo $HOME)/git/lodestar/lodestar validator --network mainnet --graffiti "${MY_GRAFFITI}"
Restart         = on-failure

[Install]
WantedBy	= multi-user.target
EOF
```

Mover el archivo de unidad a `p/systemd/system`

```bash
sudo mv $HOME/validator.service /etc/systemd/system/validator.service
```

Actualizar sus permisos.

```bash
sudo chmod 644 c/systemd/validator.service
```
{% endtab %}
{% endtabs %}

Recarga el archivo de unidad actualizado y reinicia el proceso del validador para que tu graffiti surta efecto.

{% tabs %}
{% tab title="Faro \| Prisma \| Lodestar" %}
```bash
sudo systemctl daemon-reload
sudo systemctl restart validator
```
{% endtab %}

{% tab title="Teku \| Nimbus" %}
```text
sudo systemctl daemon-reload
sudo systemctl restart beacon-chain
```
{% endtab %}
{% endtabs %}

### 📦 8.10 Actualizar un nodo ETH1 - Geth / OpenEthereum / Besu / mind

{% hint style="info" %}
De vez en cuando, asegúrese de actualizar a las últimas versiones de ETH1 para disfrutar de nuevas mejoras y características.
{% endhint %}

Detenga el proceso del nodo eth1.

```bash
# Esto puede tomar algún tiempo.
sudo systemctl stop eth1
```

Actualizar el paquete de nodos eth1 o binarios.

{% tabs %}
{% tab title="Geth" %}
Revise las últimas notas de la versión en [https://github.com/ethereum/go-ethereum/releases](https://github.com/ethereum/go-ethereum/releases)

```bash
sudo apt update
sudo apt upgrade -y
```
{% endtab %}

{% tab title="OpenEthereum \(Paridad\)" %}
Revise la última versión en [https://github.com/openethereum/openethereum/releases](https://github.com/openethereum/openethereum/releases)

Descargar automáticamente la última versión de linux, un-zip, añadir permisos de ejecución y limpieza.

```bash
cd $HOME
# copia de seguridad anterior de openethereum versión anterior en caso de rollback
mv openethereum_backup_$(date +"%Y%d%m-%H%M%S")
# almacena una nueva versión en el directorio openethreum
mkdir openethereum && cd openethereum
# download latest version
curl -s https://api.github.com/repos/openethereum/openethereum/releases/latest | jq -r ".assets[] | select(.name) | .browser_download_url" | grep linux  | xargs wget -q --show-progress
# unzip
unzip openethereum*.zip
# add execute permission
chmod +x openethereum
# limpieza
rm openethereum*.zip
```
{% endtab %}

{% tab title="Besu" %}
Revise la última versión en [https://github.com/hyperledger/besu/releases](https://github.com/hyperledger/besu/releases)

El archivo se puede descargar desde [https://dl.bintray.com/hyperledger-org/besu-repo](https://dl.bintray.com/hyperledger-org/besu-repo)

Encuentre manualmente el archivo deseado desde el repositorio anterior y modifique el comando `wget` con la URL.

> Ejemplo:
>
> wget -O besu.tar.gz [https://dl.bintray.com/hyperledger-org/besu-repo/besu-20.10.1.tar.gz](https://dl.bintray.com/hyperledger-org/besu-repo/besu-20.10.1.tar.gz)

```bash
cd $HOME
# copia de seguridad anterior de la versión besu en caso de cancelación
mv besu besu_backup_$(date +"%Y%d%m-%H%M%S")
# descargar la última besu
wget -O besu.tar.gz <https URL to latest tar.gz linux file>
# untar
tar -xvf besu.tar.gz
# limpieza
rm besu.tar.gz
# renombra besu a la ubicación de la carpeta estándar
mv besu* besu
```
{% endtab %}

{% tab title="Nethermind" %}
Revise la última versión en [https://github.com/\)\[video\] mindEth/nethermind/releases](https://github.com/NethermindEth/nethermind/releases)

Descargue automáticamente la última versión de linux, des-zip y limpieza.

```bash
cd $HOME
# copia de seguridad anterior de la versión nethermind en caso de rollback
mv nethermind_backup_$(date +"%Y%d%m-%H%M%S")
# almacenar nueva versión en el directorio nethermind
mkdir nethermind && cd nethermind 
# descargar la última versión
curl -s https://api. ithub.com/repos/)[video] mindEth/nethermind/releases/latest | jq -r ".assets[] | select(.name) | . rowser_download_url" | grep linux | xargs wget -q --show-progress
# unzip
unzip -o nethermind*.zip
# limpieza
rm nethermind*linux*.zip
```
{% endtab %}
{% endtabs %}

Inicie su proceso de nodo eth1.

```bash
sudo systemctl start eth1
```

Marque los registros para verificar que los servicios están funcionando correctamente y asegurarse de que no hay errores.

{% tabs %}
{% tab title="Faro \| Prisma \| Lodestar" %}
```bash
sudo systemctl status eth1 status beacon-chain validator
```
{% endtab %}

{% tab title="Nimbus \| Teku" %}
```text
sudo systemctl status eth1 beacon-chain
```
{% endtab %}
{% endtabs %}

Finalmente, verifique que los certificados de su validador están trabajando con el explorador de bloques público como

[https://beaconcha.in/](https://beaconcha.in/)

Introduzca la pubkey de su validador para ver su estado.

## 🌇 9. Únete a la comunidad en Discord y Reddit

### 📱 Discord

{% tabs %}
{% tab title="Lighthouse" %}
{% embed url="https://discord.gg/cyAszAh" %}
{% endtab %}

{% tab title="Nimbus" %}
{% embed url="https://discord.gg/XRxWahP" %}
{% endtab %}

{% tab title="Teku" %}
{% embed url="https://discord.gg/7hPv2T6" %}
{% endtab %}

{% tab title="Prysm" %}
{% embed url="https://discord.gg/XkyZSSk4My" %}
{% endtab %}

{% tab title="Lodestar" %}
{% embed url="https://discord.gg/aMxzVcr" %}
{% endtab %}

{% tab title="CoinCashew" %}
{% embed url="https://discord.gg/w8Bx8W2HPW" %}
{% endtab %}
{% endtabs %}

### 🌍 Reddit r/ethStaker

{% embed url="https://www.reddit.com/r/ethstaker/" caption="" %}

## 🧩10. Material de referencia

Apreciar el duro trabajo realizado por la gente fina en los siguientes enlaces que sirvieron de base para la creación de esta guía.

{% embed url="https://launchpad.ethereum.org/" caption="" %}

{% embed url="https://pegasys.tech/teku-ethereum-2-for-world-e/" caption="" %}

{% embed url="https://docs.teku.pegasys.tech/es/latest/howTo/Get-Started/Build-From-Source/" caption="" %}

{% embed url="https://lighthouse-book.sigmaprime.io/intro.html" caption="" %}

{% embed url="https://status-im.github.io/nimbus-eth2/intro.html" caption="" %}

{% embed url="https://prylabs.net/participate" caption="" %}

{% embed url="https://docs.prylabs.network/docs/getting-started/" caption="" %}

{% embed url="https://chainsafe.github.io/lodestar/installation/" caption="" %}

## 🎉11. Enlaces de bonus

### 🧱 Exploradores de Bloques ETH2

{% embed url="https://beaconcha.in/" caption="" %}

{% embed url="https://beaconscan.com/" caption="" %}

### 🗒 Última información de Eth2

{% embed url="https://hackmd.io/@benjaminion/eth2\_news/" caption="" %}

{% embed url="https://www.reddit.com/r/ethstaker" caption="" %}

{% embed url="https://blog.ethereum.org/" caption="" %}

### 👨👩👧 Guías adicionales de la comunidad ETH2

{% embed url="https://someresat.medium.com/" caption="" %}

{% embed url="https://github.com/metanull-operator/eth2-ubuntu" caption="" %}

{% embed url="https://agstakingco.gitbook.io/eth-2-0-staking-medalla/" caption="" %}

#### Guía de Hardware [https://www.reddit.com/r/ethstaker/comments/j3mlup/a\_→ tly\_updated\_look\_at\_hardware\_for\_staking/](https://www.reddit.com/r/ethstaker/comments/j3mlup/a_slightly_updated_look_at_hardware_for_staking/)

{% embed url="https://medium.com/@RaymondDurk/how-to-stake-for-ethereum-2-0-with-dappnode-231fa7689c02" caption="" %}

{% embed url="https://kb.beaconcha.in/" caption="" %}
