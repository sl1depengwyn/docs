---
description: '?module=contract'
---

# Contract

{% hint style="info" %}
Page is under construction. For a full description of RPC endpoints, visit [https://blockscout.com/xdai/mainnet/api-docs](https://blockscout.com/xdai/mainnet/api-docs)
{% endhint %}

### &#x20;`https://instance_base_url/api?module=contract`

## Get a list of contracts

`listcontracts`

List sorted in ascending order based on the time a contact was first indexed by the explorer. With filters \`not\_decompiled\`(\`4\`) or \`not\_verified(4)\` the results will not be sorted for performance reasons.

**Example:**

```
https://instance_base_url/api
   ?module=contract
   &action=listcontracts
```

{% tabs %}
{% tab title="Request Params" %}
| Parameter                      | Description                                                                                                                                                                                                              |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| page                           | <mark style="background-color:yellow;">optional</mark> nonnegative `integer` representing the page number used for pagination. 'offset' must also be provided.                                                           |
| offset                         | <mark style="background-color:yellow;">optional</mark> nonnegative `integer` representing the max number of records to return when paginating. 'page' must also be provided.                                             |
| filter                         | <mark style="background-color:yellow;">optional</mark>  string `verified`\|`decompiled`\|`unverified`\|`not_decompiled`\|`empty`, or `1`\|`2`\|`3`\|`4`\|`5` respectively. Returns  contracts with the requested status. |
| not\_decompiled\_with\_version | <mark style="background-color:yellow;">optional</mark> `string` ensures none of the returned contracts were decompiled with the provided version. Ignored unless filtering for `decompiled` contracts.                   |
| verified\_at\_start\_timestamp | <mark style="background-color:yellow;">optional</mark>  `unix timestamp` Represents the starting timestamp for verified contracts. Only used with `verified` filter.                                                     |
| verified\_at\_end\_timestamp   | <mark style="background-color:yellow;">optional</mark> `unix timestamp` Represents the ending timestamp for verified contracts. Only used with `verified` filter.                                                        |
{% endtab %}

{% tab title="Example Result" %}
```json
{
  "message": "OK",
  "result": [
    {
      "ABI": "[{\n\"type\":\"event\",\n\"inputs\": [{\"name\":\"a\",\"type\":\"uint256\",\"indexed\":true},{\"name\":\"b\",\"type\":\"bytes32\",\"indexed\":false}],\n\"name\":\"Event\"\n}, {\n\"type\":\"event\",\n\"inputs\": [{\"name\":\"a\",\"type\":\"uint256\",\"indexed\":true},{\"name\":\"b\",\"type\":\"bytes32\",\"indexed\":false}],\n\"name\":\"Event2\"\n}, {\n\"type\":\"function\",\n\"inputs\": [{\"name\":\"a\",\"type\":\"uint256\"}],\n\"name\":\"foo\",\n\"outputs\": []\n}]\n",
      "CompilerVersion": "v0.2.1-2016-01-30-91a6b35",
      "ContractName": "Test",
      "OptimizationUsed": "1",
      "SourceCode": "pragma solidity >0.4.24;\n\ncontract Test {\nconstructor() public { b = hex\"12345678901234567890123456789012\"; }\nevent Event(uint indexed a, bytes32 b);\nevent Event2(uint indexed a, bytes32 b);\nfunction foo(uint a) public { emit Event(a, b); }\nbytes32 b;\n}\n"
    }
  ],
  "status": "1"
}
```
{% endtab %}
{% endtabs %}

## Get ABI for a verified contract

`getabi`

Also available through a GraphQL `addresses` query.&#x20;

**Example:**

```
https://instance_base_url/api
   ?module=contract
   &action=getabi
   &address={addressHash}
```

{% tabs %}
{% tab title="Request Params" %}
| Parameter   |  Description                          |
| ----------- | ------------------------------------- |
| **address** | `string` containing the address hash. |
{% endtab %}

{% tab title="Example Result" %}
```
{
  "message": "OK",
  "result": "[{\"constant\":false,\"inputs\":[{\"name\":\"voucher_token\",\"type\":\"bytes32\"}],\"name\":\"burn\",\"outputs\":[{\"name\":\"success\",\"type\":\"bool\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[{\"name\":\"voucher_token\",\"type\":\"bytes32\"}],\"name\":\"is_expired\",\"outputs\":[{\"name\":\"\",\"type\":\"bool\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"voucher_token\",\"type\":\"bytes32\"}],\"name\":\"is_burnt\",\"outputs\":[{\"name\":\"\",\"type\":\"bool\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"inputs\":[{\"name\":\"voucher_token\",\"type\":\"bytes32\"},{\"name\":\"_lifetime\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"constructor\"}]",
  "status": "1"
}
```
{% endtab %}
{% endtabs %}



## Get contract source code for a verified contract

`getsourcecode`

Also available through a GraphQL `addresses` query.&#x20;

**Example:**

```
https://instance_base_url/api
   ?module=contract
   &action=getsourcecode
   &address={addressHash}
```

{% tabs %}
{% tab title="Request Params" %}
| Parameter   |  Description                          |
| ----------- | ------------------------------------- |
| **address** | `string` containing the address hash. |
{% endtab %}

{% tab title="Example Result" %}
```
{
  "message": "OK",
  "result": {
    "ABI": "[{\n\"type\":\"event\",\n\"inputs\": [{\"name\":\"a\",\"type\":\"uint256\",\"indexed\":true},{\"name\":\"b\",\"type\":\"bytes32\",\"indexed\":false}],\n\"name\":\"Event\"\n}, {\n\"type\":\"event\",\n\"inputs\": [{\"name\":\"a\",\"type\":\"uint256\",\"indexed\":true},{\"name\":\"b\",\"type\":\"bytes32\",\"indexed\":false}],\n\"name\":\"Event2\"\n}, {\n\"type\":\"function\",\n\"inputs\": [{\"name\":\"a\",\"type\":\"uint256\"}],\n\"name\":\"foo\",\n\"outputs\": []\n}]\n",
    "CompilerVersion": "v0.2.1-2016-01-30-91a6b35",
    "ContractName": "Test",
    "FileName": "{sourcify path or empty}",
    "ImplementationAddress": "0x000000000000000000000000000000000000000e",
    "IsProxy": "true",
    "OptimizationUsed": "1",
    "SourceCode": "pragma solidity >0.4.24;\n\ncontract Test {\nconstructor() public { b = hex\"12345678901234567890123456789012\"; }\nevent Event(uint indexed a, bytes32 b);\nevent Event2(uint indexed a, bytes32 b);\nfunction foo(uint a) public { emit Event(a, b); }\nbytes32 b;\n}\n"
  },
  "status": "1"
}
```
{% endtab %}
{% endtabs %}



## Verify a contract with its source code and contract creation information

`verify`

**Example:**

```
https://instance_base_url/api
   ?module=contract
   &action=verify
   &addressHash={addressHash}
   &name={name}
   &compilerVersion={compilerVersion}
   &optimization={false}
   &contractSourceCode={contractSourceCode}
```

**Curl Post Example**

{% code overflow="wrap" %}
```
curl -d '{"addressHash":"0xc63BB6555C90846afACaC08A0F0Aa5caFCB382a1","compilerVersion":"v0.5.4+commit.9549d8ff", "contractSourceCode":"pragma solidity ^0.5.4; contract Test { }","name":"Test","optimization":false}' -H "Content-Type: application/json" -X POST "https://blockscout.com/poa/sokol/api?module=contract&action=verify"
```
{% endcode %}

{% hint style="info" %}
On successful submission you will receive a guid as a receipt. Use this with [`checkverifystatus`](contract.md#return-status-of-a-verification-attempt)`to view verification status.`
{% endhint %}

{% tabs %}
{% tab title="Params" %}
| Parameter                      | Description                                                                                                                |
| ------------------------------ | -------------------------------------------------------------------------------------------------------------------------- |
| **addressHash**                | `string` containing the address hash of the contract.                                                                      |
| **name**                       | `string` containing the name of the contract.                                                                              |
| **compilerVersion**            | `string` containing the compiler version for the contract.                                                                 |
| **optimization**               | `enum` whether or not compiler optimizations were enabled `0`=false, `1`=true                                              |
| **contractSourceCode**         | `string` containing the source code of the contract.                                                                       |
| constructorArguments           | <mark style="background-color:yellow;">optional</mark>  `string` constructor argument data provided.                       |
| autodetectConstructorArguments | <mark style="background-color:yellow;">optional</mark> `boolean` whether or not automatically detect constructor argument. |
| evmVersion                     | <mark style="background-color:yellow;">optional</mark>  EVM version for the contract.                                      |
| optimizationRuns               | <mark style="background-color:yellow;">optional</mark> number of optimization runs used during compilation                 |
| library1Name                   | <mark style="background-color:yellow;">optional</mark> `string` name of the first library used.                            |
| library1Address                | <mark style="background-color:yellow;">optional</mark> `string` address of the first library used.                         |
| library2Name                   | <mark style="background-color:yellow;">optional</mark> `string` name of the second library used.                           |
| library2Address                | <mark style="background-color:yellow;">optional</mark> `string` address of the second library used.                        |
| library3Name                   | <mark style="background-color:yellow;">optional</mark> `string` name of the third library used.                            |
| library3Address                | <mark style="background-color:yellow;">optional</mark> `string` address of the third library used.                         |
| library4Name                   | <mark style="background-color:yellow;">optional</mark> `string` name of the fourth library used.                           |
| library4Address                | <mark style="background-color:yellow;">optional</mark> `string` address of the fourth library used.                        |
| library5Name                   | <mark style="background-color:yellow;">optional</mark> `string` name of the fifth library used.                            |
| library5Address                | <mark style="background-color:yellow;">optional</mark> `string` address of the fifth library used.                         |
{% endtab %}

{% tab title="Example Result" %}
{% code overflow="wrap" %}
```
{
  "message": "OK",
  "result": {
    "ABI": "[{\n\"type\":\"event\",\n\"inputs\": [{\"name\":\"a\",\"type\":\"uint256\",\"indexed\":true},{\"name\":\"b\",\"type\":\"bytes32\",\"indexed\":false}],\n\"name\":\"Event\"\n}, {\n\"type\":\"event\",\n\"inputs\": [{\"name\":\"a\",\"type\":\"uint256\",\"indexed\":true},{\"name\":\"b\",\"type\":\"bytes32\",\"indexed\":false}],\n\"name\":\"Event2\"\n}, {\n\"type\":\"function\",\n\"inputs\": [{\"name\":\"a\",\"type\":\"uint256\"}],\n\"name\":\"foo\",\n\"outputs\": []\n}]\n",
    "CompilerVersion": "v0.2.1-2016-01-30-91a6b35",
    "ContractName": "Test",
    "ImplementationAddress": "0x000000000000000000000000000000000000000e",
    "IsProxy": "true",
    "OptimizationUsed": "1",
    "SourceCode": "pragma solidity >0.4.24;\n\ncontract Test {\nconstructor() public { b = hex\"12345678901234567890123456789012\"; }\nevent Event(uint indexed a, bytes32 b);\nevent Event2(uint indexed a, bytes32 b);\nfunction foo(uint a) public { emit Event(a, b); }\nbytes32 b;\n}\n"
  },
  "status": "1"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Verify a contract through [Sourcify](https://sourcify.dev/)

`verify_via_sourcify`

1. if a smart contract is already verified on Sourcify, it will automatically fetch the data from the [repo](https://repo.sourcify.dev/)
2. otherwise you need to upload source files and JSON metadata file(s).

**Example:**

```
https://instance_base_url/api
 ?module=contract
 &action=verify_via_sourcify
 &addressHash={addressHash}
```

#### POST body example

```
--6e1e4c11657c62dc1e4349d024de9e28
Content-Disposition: form-data; name="addressHash"

0xb77b7443e0F32F1FEBf0BE0fBd7124D135d0a525

--6e1e4c11657c62dc1e4349d024de9e28
Content-Disposition: form-data; name="files[0]"; filename="contract.sol"
Content-Type: application/json

...Source code...

--6e1e4c11657c62dc1e4349d024de9e28
Content-Disposition: form-data; name="files[1]"; filename="metadata.json"
Content-Type: application/json

...JSON metadata...

--6e1e4c11657c62dc1e4349d024de9e28--
```

{% tabs %}
{% tab title="Params" %}
| Parameter       |  Description                            |
| --------------- | --------------------------------------- |
| **addressHash** | `string` containing the address hash.   |
| files           | `array` with sources and metadata files |
{% endtab %}

{% tab title="Example " %}
```
{
  "message": "OK",
  "result": {
    "ABI": "[{\n\"type\":\"event\",\n\"inputs\": [{\"name\":\"a\",\"type\":\"uint256\",\"indexed\":true},{\"name\":\"b\",\"type\":\"bytes32\",\"indexed\":false}],\n\"name\":\"Event\"\n}, {\n\"type\":\"event\",\n\"inputs\": [{\"name\":\"a\",\"type\":\"uint256\",\"indexed\":true},{\"name\":\"b\",\"type\":\"bytes32\",\"indexed\":false}],\n\"name\":\"Event2\"\n}, {\n\"type\":\"function\",\n\"inputs\": [{\"name\":\"a\",\"type\":\"uint256\"}],\n\"name\":\"foo\",\n\"outputs\": []\n}]\n",
    "CompilerVersion": "v0.2.1-2016-01-30-91a6b35",
    "ContractName": "Test",
    "ImplementationAddress": "0x000000000000000000000000000000000000000e",
    "IsProxy": "true",
    "OptimizationUsed": "1",
    "SourceCode": "pragma solidity >0.4.24;\n\ncontract Test {\nconstructor() public { b = hex\"12345678901234567890123456789012\"; }\nevent Event(uint indexed a, bytes32 b);\nevent Event2(uint indexed a, bytes32 b);\nfunction foo(uint a) public { emit Event(a, b); }\nbytes32 b;\n}\n"
  },
  "status": "1"
}
```
{% endtab %}
{% endtabs %}



## Verify a vyper contract with its source code and contract creation information

`verify_vyper_contract`

**Example**

```
https://instance_base_url/api
 ?module=contract
 &action=verify_vyper_contract
 &addressHash={addressHash}
 &name={name}
 &compilerVersion={compilerVersion}
 &contractSourceCode={contractSourceCode}
```

**curl POST example**

{% code overflow="wrap" %}
```
curl --location --request POST 'http://localhost:4000/api?module=contract&action=verify_vyper_contract' --form 'contractSourceCode="SOURCE_CODE"' --form 'name="Vyper_contract"' --form 'addressHash="0xE60B1B8bD493569a3E945be50A6c89d29a560Fa1"' --form 'compilerVersion="v0.2.12"'
```
{% endcode %}

{% tabs %}
{% tab title="First Tab" %}


| Parameter              | Description                                                |
| ---------------------- | ---------------------------------------------------------- |
| **addressHash**        | `string` containing the address hash of the contract.      |
| **name**               | `string` containing the name of the contract.              |
| **compilerVersion**    | `string` containing the compiler version for the contract. |
| **contractSourceCode** | `string` containing the source code of the contract.       |
| constructorArguments   | `string` constructor argument data provided.               |
{% endtab %}

{% tab title="Example" %}
```
{
  "message": "OK",
  "result": {
    "ABI": "[{\n\"type\":\"event\",\n\"inputs\": [{\"name\":\"a\",\"type\":\"uint256\",\"indexed\":true},{\"name\":\"b\",\"type\":\"bytes32\",\"indexed\":false}],\n\"name\":\"Event\"\n}, {\n\"type\":\"event\",\n\"inputs\": [{\"name\":\"a\",\"type\":\"uint256\",\"indexed\":true},{\"name\":\"b\",\"type\":\"bytes32\",\"indexed\":false}],\n\"name\":\"Event2\"\n}, {\n\"type\":\"function\",\n\"inputs\": [{\"name\":\"a\",\"type\":\"uint256\"}],\n\"name\":\"foo\",\n\"outputs\": []\n}]\n",
    "CompilerVersion": "v0.2.1-2016-01-30-91a6b35",
    "ContractName": "Test",
    "ImplementationAddress": "0x000000000000000000000000000000000000000e",
    "IsProxy": "true",
    "OptimizationUsed": "1",
    "SourceCode": "pragma solidity >0.4.24;\n\ncontract Test {\nconstructor() public { b = hex\"12345678901234567890123456789012\"; }\nevent Event(uint indexed a, bytes32 b);\nevent Event2(uint indexed a, bytes32 b);\nfunction foo(uint a) public { emit Event(a, b); }\nbytes32 b;\n}\n"
  },
  "status": "1"
}
```
{% endtab %}
{% endtabs %}

## Verify a contract with Standard input JSON file

`verifysourcecode`

**Example**

```
https://instance_base_url/api
 ?module=contract
 &action=verifysourcecode
 &codeformat={solidity-standard-json-input}
 &contractaddress={contractaddress}
 &contractname={contractname}
 &compilerversion={compilerversion}
 &sourceCode={sourceCode}
```

{% tabs %}
{% tab title="Params" %}


| Parameter                      | Description                                                                                                                                                                    |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **codeformat**                 | Format of sourceCode (currently only supports `solidity-standard-json-input`)                                                                                                  |
| **contractaddress**            | `string` containing the address hash of the contract.                                                                                                                          |
| **contractname**               | `string` name of the contract. It an be an empty string(""), just the contract name("ContractName"), or a filename and contract name("contracts/contract\_1.sol:ContractName") |
| **compilerversion**            | `string` containing the compiler version for the contract.                                                                                                                     |
| **sourceCode**                 | `string` standard input json                                                                                                                                                   |
| constructorArguments           | <mark style="background-color:yellow;">optional</mark> `string` constructor argument data provided.                                                                            |
| autodetectConstructorArguments | <mark style="background-color:yellow;">optional</mark> `boolean` whether or not automatically detect constructor argument.                                                     |
{% endtab %}

{% tab title="Example Result" %}
```
{
  "message": "OK",
  "result": "b080b96bd06ad1c9341c2afb7e3730311388544961acde94",
  "status": "1"
}
```
{% endtab %}
{% endtabs %}

## Return status of a verification attempt

`checkverifystatus`

{% hint style="info" %}
guid is received as a receipt from the `verifysourcecode` method.
{% endhint %}

**Example**

```
https://instance_base_url/api
 ?module=contract
 &action=checkverifystatus
 &guid={identifierString}
```

{% tabs %}
{% tab title="Params" %}
| Parameter |  Description                                      |
| --------- | ------------------------------------------------- |
| **guid**  | `string`used for identifying verification attempt |
{% endtab %}

{% tab title="Example Result" %}
```
{
  "message": "OK",
  "result": "Pending in queue",
  "status": "1"
}
```

{% hint style="info" %}
Return Options: `Pending in queue` | `Pass - Verified` | `Fail - Unable to verify` | `Unknown UID`
{% endhint %}
{% endtab %}
{% endtabs %}
