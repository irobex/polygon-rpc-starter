## polygon-rpc-starter

Быстрый старт Polygon RPC: примеры, тарифы, бесплатный ключ `fastpolygon.tech`.

### Endpoint
Формат:
- `https://rpc.fastpolygon.tech/v1/{API_KEY}`

### Примеры

#### curl

```bash
API_KEY="ВАШ_КЛЮЧ"

curl -sS -X POST "https://rpc.fastpolygon.tech/v1/${API_KEY}" \
  -H 'Content-Type: application/json' \
  --data '{"jsonrpc":"2.0","id":1,"method":"eth_blockNumber","params":[]}'
```

#### Node.js (ethers v6)

```bash
npm i ethers
```

```js
import { JsonRpcProvider } from "ethers";

const API_KEY = process.env.FP_API_KEY;
if (!API_KEY) throw new Error("Set FP_API_KEY");

const provider = new JsonRpcProvider(`https://rpc.fastpolygon.tech/v1/${API_KEY}`);

console.log(await provider.getBlockNumber());
```

### Тарифы fastpolygon.tech
- Free: 100k req/мес, 3 RPS, 1 key
- Starter $10: 1M req/мес, 10 RPS, 1 key
- Pro $25: 5M req/мес, 25 RPS, 2 keys
- Heavy $50: 20M req/мес, 50 RPS, 3 keys

### Где взять ключ
Откройте `https://app.fastpolygon.tech` → введите email → получите код → создайте ключ в кабинете.


