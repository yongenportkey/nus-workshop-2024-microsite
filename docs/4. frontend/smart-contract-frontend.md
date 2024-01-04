---
title: Smart Contract on Frontend
sidebar_position: 2
---

# Smart Contract on Frontend

Now that a smart contract has been deployed successfully, it might be desireable to call the smart contract on the frontend.

This example will demonstrate how to do this.

## 1. Add new files

### 1.1. Add a new file `src/useSmartContract.ts` and copy/paste the following:

:::warning

Amend the address highlighted below to your own.

:::

```ts title="src/useSmartContract.ts" showLineNumbers
import { IPortkeyProvider, IChain } from "@portkey/provider-types";
import { useEffect, useState } from "react";

export type IContract = ReturnType<IChain["getContract"]>;

function useSmartContract(provider: IPortkeyProvider | null) {
  const [smartContract, setSmartContract] = useState<IContract>();

  useEffect(() => {
    (async () => {
      if (!provider) return null;

      try {
        // 1. get the sidechain tDVW using provider.getChain
        const chain = await provider?.getChain("tDVW");
        if (!chain) throw new Error("No chain");

        const address = "4CknAAWUdByDxrHVPM3F1PGPGSgwaFt7mSapxBifqsipMfqpm"; // replace with your deployed contract address

        // 2. get the contract
        const contract = chain?.getContract(address);
        setSmartContract(contract);
      } catch (error) {
        console.log(error, "====error");
      }
    })();
  }, [provider]);

  return smartContract;
}

export default useSmartContract;
```

### 1.2. Add a new file `src/SmartContract.tsx` and copy/paste the following:

```tsx title="src/SmartContract.tsx" showLineNumbers
import { IPortkeyProvider, MethodsBase } from "@portkey/provider-types";
import useSmartContract from "./useSmartContract";
import { useState } from "react";

function SmartContract({ provider }: { provider: IPortkeyProvider | null }) {
  const contract = useSmartContract(provider);
  const [mintAccount, setMintAccount] = useState("");

  const onInitialize = async () => {
    const accounts = await provider?.request({
      method: MethodsBase.ACCOUNTS,
    });
    if (!accounts) throw new Error("No accounts");

    const account = accounts?.tDVW?.[0]!;
    if (!account) throw new Error("No account");

    return await contract?.callSendMethod("Initialize", account, {
      Symbol: "symbol",
      MintStartTime: "",
      MintEndTime: "",
      NftImageUrl:
        "https://i.seadn.io/gcs/files/0f5cdfaaf687de2ebb5834b129a5bef3.png?auto=format&w=3840",
      EventTitle: "WORKSHOP",
      EventDate: "20240101",
      EventVenue: "COM3",
      EventDescription: "A WORKSHOP",
    });
  };

  const onMint = async () => {
    return await contract?.callSendMethod("Mint", mintAccount, {});
  };

  if (!provider) return null;

  return (
    <div>
      <button onClick={onInitialize}>Initialize</button>
      <input
        value={mintAccount}
        onChange={(e) => setMintAccount(e.target.value)}
      />
      <button onClick={onMint}>Mint</button>
    </div>
  );
}

export default SmartContract;
```

## 2. Edit `src/App.tsx`:

```tsx title="src/App.tsx" showLineNumbers
import { useEffect, useState } from "react";
import { IPortkeyProvider, MethodsBase } from "@portkey/provider-types";
import "./App.css";
import detectProvider from "@portkey/detect-provider";
import Balance from "./Balance";
import Nft from "./Nft";
// highlight-next-line
import SmartContract from "./SmartContract";

function App() {
  const [provider, setProvider] = useState<IPortkeyProvider | null>(null);

  const init = async () => {
    try {
      setProvider(await detectProvider());
    } catch (error) {
      console.log(error, "=====error");
    }
  };

  const connect = async () => {
    await provider?.request({
      method: MethodsBase.REQUEST_ACCOUNTS,
    });
  };

  useEffect(() => {
    if (!provider) init();
  }, [provider]);

  if (!provider) return <>Provider not found.</>;

  return (
    <>
      <button onClick={connect}>Connect</button>
      // highlight-next-line
      <SmartContract provider={provider} />
    </>
  );
}

export default App;
```

After Sign in, click on the `Initialize` button.

Fill in the address for mint, then click on the `Mint` button.
