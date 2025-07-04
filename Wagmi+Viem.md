地址：<https://www.helloworld.net/p/7641297058>

**使用 Wagmi 2.0 和 Viem 的教程**

Wagmi 2.0 是一个全新的版本，采用了 Viem 作为底层库，使得以太坊应用程序开发变得更加高效和便捷。Viem 是一个用于与以太坊区块链交互的库，提供了更快、更可靠的操作，并且更好地支持 TypeScript。

步骤：
- 1、安装：`npm install wagmi viem@2.x @tanstack/react-query`
- 2、配置config：
```
import { http, createConfig } from 'wagmi'
import { mainnet, sepolia } from 'wagmi/chains'

export const config = createConfig({
  chains: [mainnet, sepolia],
  transports: {
    [mainnet.id]: http(),
    [sepolia.id]: http(),
  },
})
```
- 3、添加providers：
```
import { QueryClient, QueryClientProvider } from '@tanstack/react-query'
import { WagmiProvider } from 'wagmi'
import { config } from './config'

const queryClient = new QueryClient()

function App() {
  return (
    <WagmiProvider config={config}>
      <QueryClientProvider client={queryClient}>
        {/** ... */}
      </QueryClientProvider>
    </WagmiProvider>
  )
}
```
- 4、连接钱包：Wagmi 2.0 提供了便捷的方式来连接用户的加密钱包，比如 MetaMask。下面是一个简单的连接钱包的示例：
```
import { useAccount, useConnect, useDisconnect } from 'wagmi';
import { InjectedConnector } from 'wagmi/connectors/injected';

const ConnectWallet = () => {
  const { address, isConnected } = useAccount();
  const { connect } = useConnect({
    connector: new InjectedConnector(),
  });
  const { disconnect } = useDisconnect();

  if (isConnected) {
    return (
      <div>
        <p>Connected to {address}</p>
        <button onClick={() => disconnect()}>Disconnect</button>
      </div>
    );
  }

  return <button onClick={() => connect()}>Connect Wallet</button>;
};
```
