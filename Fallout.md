### My Aim
Claim the ownership of the contract.

### Approach:
1. First the conract uses older solidity version which 0.6.0 where we declare the constructor with the same name as contract.
2. I try to find where it set the owner state variable which is in the constructor.
```sh
  /* constructor */
  function Fal1out() public payable {
    owner = msg.sender;
    allocations[owner] = msg.value;
  }
```
3. But if you look closely it's not a constructor because it's name is Fal1back and contract name is Fallback.
4. So if we deploy the contract it will set the owner address to 0 because it will never call the constructor.
5. But we call the the Fal1back function through the contract instance which will set the ownership to msg.sender which is attacker address and claim the ownership.