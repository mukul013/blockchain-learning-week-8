### My Aim
Claim the ownership & reduce the balance to zero.

### Approach:
1. First I look where owner state variable is set and found the receive function.
```sh
  receive() external payable {
    require(msg.value > 0 && contributions[msg.sender] > 0);
    owner = msg.sender;
  }
```
2. In receive funciton I see I need to send some amount of ether and contributions[msg.sender] > 0.
3. Now contributions variable is set by contribute function.
```sh
  function contribute() public payable {
    require(msg.value < 0.001 ether);
    contributions[msg.sender] += msg.value;
    if(contributions[msg.sender] > contributions[owner]) {
      owner = msg.sender;
    }
  }
```
4. Now first I have to call the contribute function to set contributions variable to set it's value greater than 0.
5. Then we'll call function receive which will set us the owner of the contract.
6. Then we'll be able to call be function withdraw which will withdraw all the ether from this contract.
```sh
  function withdraw() public onlyOwner {
    payable(owner).transfer(address(this).balance);
  }
```