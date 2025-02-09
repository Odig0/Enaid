# Enaid WhatsAppBot Financiero

Este bot de WhatsApp combina la potencia de [Baileys](https://github.com/adiwajshing/Baileys) con [AgentKit de Coinbase](https://portal.cdp.coinbase.com/access/api) para realizar transacciones financieras, gestionar billeteras y ejecutar compras directamente a través de WhatsApp.

## Características Principales

- **Operaciones Financieras:** Integra AgentKit de Coinbase para permitir transferencias y compras de activos digitales.
- **Basado en Baileys:** Conexión estable con WhatsApp para enviar y recibir mensajes.
- **Gestión de Datos:** Se puede configurar con [Supabase](https://supabase.com/) para almacenar información de usuarios y transacciones.
- **Arquitectura en TypeScript:** Código tipado para mayor confiabilidad y escalabilidad.
- **Soporte para Docker:** Incluye `docker-compose.yml` para simplificar la implementación.

## Requisitos

- **Node.js 14+**
- [AgentKit de Coinbase](https://portal.cdp.coinbase.com/access/api) con sus claves de API
- [Supabase CLI](https://supabase.com/docs/guides/cli) (opcional, para gestionar la base de datos)
- [Docker](https://www.docker.com/) (opcional, para desplegar en contenedores)

### Verificar Versión de Node.js

Ejecute los siguientes comandos para comprobar su versión de Node.js y pnpm:

```bash
node --version
pnpm --version
```

## Instalación

1. **Clonar el repositorio:**
```bash
git clone https://github.com/Odig0/Enaid.git
cd Enaid
```
2. **Instalar dependencias:**
```bash
pnpm install
```

## Configuración de Variables de Entorno

Cree o edite un archivo `.env` en la raíz del proyecto con las siguientes variables:

```env
GOOGLE_CLIENT_EMAIL=NO
GOOGLE_PRIVATE_KEY=NO
DATABASE_HOST=localhost
DATABASE_NAME=WhatsappBot
DATABASE_PASSWORD=postgres
DATABASE_USERNAME=postgres
DATABASE_URL=postgres://postgres:postgres@localhost/WhatsappBot
CDP_API_KEY_NAME=""
CDP_API_KEY_PRIVATE_KEY=""
OPENAI_API_KEY=""
```

> Ajuste estos valores según sus credenciales y configuración.

## Ejecución del Bot

### Modo Desarrollo

```bash
pnpm run dev
```

Al iniciar, se generará un **código QR** en la terminal. Escanéelo con WhatsApp en la sección **WhatsApp Web** para vincular su cuenta.

### Escaneo de Código QR

Una vez vinculado, el bot podrá enviar y recibir mensajes. Por ejemplo, puede consultar su saldo o iniciar una transacción:

```bash
!balance
!transfer 0.01ETH to 0x12345...
```

El bot utilizará AgentKit de Coinbase para realizar la operación.

### Uso con Docker

Si desea usar Docker, ejecute:

```bash
docker-compose up
```

Esto iniciará el servicio dentro de un contenedor con todas las dependencias configuradas.

## Funding de Billetera (Faucet)

Si estás en Base Sepolia o una testnet compatible, puedes añadir fondos a tu billetera mediante una faucet. Por ejemplo, ejecuta:

```bash
/coinbase faucet
```

El bot esperará a que la transacción se confirme on-chain y te notificará cuando esté completada:

```bash
Faucet transaction completed successfully.
```

Para verificar tu saldo:

```bash
/coinbase balance
```

## Transferencia de Fondos

Una vez que tu billetera tiene fondos, puedes transferirlos a otra cuenta. Si deseas transferir a tu billetera de MetaMask, por ejemplo `0x77370fd2f08c9ea9E439460C8Ced941627957065`, utiliza:

```bash
/coinbase transfer 0.00001 ETH to 0x77370fd2f08c9ea9E439460C8Ced941627957065
```

El bot confirmará cuando la transacción se haya completado con éxito.

## Ejemplos de Comandos

- **Consultar Saldo:**

```bash
/coinbase balance
```

Muestra el saldo de la billetera configurada.

- **Transferir Activos:**

```bash
/coinbase transfer 0.05ETH to 0xABCDEF...
```

Realiza una transferencia de la cantidad especificada de ETH a la dirección elegida.

- **Comprar Tokens:**

```bash
/coinbase buy TOKEN_SYMBOL cantidad
```

Ejecuta una compra de activos utilizando AgentKit.

- **Consultar Dirección:**

```bash
/coinbase cual es mi address
```

El bot responderá con la información de tu cuenta y la dirección configurada:

```
Bot: Wallet: 38693f84-b674-457d-a773-83c2d1ed77bd en la red base-sepolia
Dirección predeterminada: 0x644dC3a1C26e7747c47b7dF216646Df7a765CA35
Tu dirección es: 0x644dC3a1C26e7747c47b7dF216646Df7a765CA35
```

## Contribuciones

Contribuciones son bienvenidas. Para proponer mejoras:

1. Haga un *fork* del repositorio.
2. Cree una nueva rama:
```bash
git checkout -b feature/nueva-funcionalidad
```
3. Realice sus cambios y *commits*.
4. Abra un *Pull Request* describiendo en detalle sus aportes.

## Licencia

Este proyecto se distribuye bajo la Licencia **MIT**.
