# Sourcify Plugin for Hardhat

Similar to the  [hardhat verification plugin, ](hardhat-verification-plugin.md)this plugin submits the contract source and other info of all deployed contracts to Sourcify.

1\) **Tune Hardhat environment**. For seamless usage, you should setup your environment [following this tutorial ](https://github.com/wighawag/tutorial-hardhat-deploy)(note, it will take an hour or so to run through). In this example we setup to use the Sokol test network.  See the[ Hardhat Verification Tutorial for more information on the config file setup](hardhat-verification-plugin.md#config-file).

2\) **Deploy contract**. [More deployment details here](https://github.com/wighawag/tutorial-hardhat-deploy#7-deploying-to-a-live-network). Note that we run from `node_modules.bin\hardhat` to circumvent package.json warning and use `--network sokol` to specify the network.

```bash
D:\test>yarn hardhat --network sokol deploy
yarn run v1.22.17 
warning package.json: No license field 
$ D:\test\node_modules.bin\hardhat --network sokol deploy 
Nothing to compile deploying "Greeter" (tx: 0x32d11b11a547c126a4763be963f6acd0bb4f87ee7d7627e36f7d9009c57c6182)...: deployed at 0xBEA47De7132cF44D6b16617154CAA247b6568eaD with 528275 gas 
Done in 18.81s.
```

3\) **Verify contract**.&#x20;

```bash
D:\test>yarn hardhat --network sokol sourcify
yarn run v1.22.17
warning package.json: No license field
$ D:\test\node_modules\.bin\hardhat --network sokol sourcify
verifying Greeter (0xBEA47De7132cF44D6b16617154CAA247b6568eaD on chain 77) ...
 => contract Greeter is now verified
Done in 5.74s.
```

4\) **Confirm verification in BlockScout**. Go to your BlockScout instance and paste the contract address into the search bar. If verified, the code tab will display a green checkmark.

![](../../.gitbook/assets/verified-1.png)

**Selecting the Code tab will show additional information about your contract.**

![](../../.gitbook/assets/verify-2.png)

