## Ali_Khatami_Solidity_3
### Basic Errors and Warnings

Here is a code that contains errors.<br>
```
//SPDX-License-Identifier: MIT
pragma solidity ^0.8.7;

contract akrkSimplestorage {
  // basic data types: boolean, uint,int,address,bytes
  //uint(unsigned integer only positive),int both pos and neg
  //address is the address of the account
  //string are secretly byte objects only for text
  //bytes32 is a bytes objects whre 32 represent how many bytes we want them to be,max size is 32
  //byte objects look like 0xsdsysydggt
  //unint256 here 256 is bit (8,16,32 upto 256 we can use)
  uint256 preferredNumber;//remove public so that we don't get duplicate functions at the moment we will just get the retrieve function
   //if we have whole bunch of variables inside the contract akrkSimplestorage those actually get indexed
   //here 'uint256 preferredNumber' will get index to 'zero'
  
//Below we have created a new type in our solidity that holds both preferred number and name 
  struct Individuals{
    uint256 preferredNumber;//this get indexed to 0
    string name;// this get indexexd to 1
//whenever we have list of variables inside an object they automatically get indexed

}

  // here below we create an array of uint256 and now preferred number can be a list or array
  //uint256[] public preferredNumbersList;

//here below we want an array of Individuals we give it visibility of public and variable name individuals
  Individuals[] public individuals; //it is automatically giving a view function and it will give nothing if it is empty and in it's button the value that it wants is gonna be the index of the object
// array above is a dynamic array because size of the array is not given at it's initialization if we don't add any size it can be any size and here we gonna work with dynamic array

//pasing parameter of type uint256 and made the function public
  function store(uint256 _preferredNumber) public{
      preferredNumber = _preferredNumber;
    
  }

  function retrieve() public view returns(uint256){
    return preferredNumber;
  }

  //now we will create a function that is going to add individuals to Individual array
  function addCitizen(string memory _name, uint256 _preferredNumber) public {
      
      individuals.push(Individuals(_preferredNumber,_name))//Here we have created a push function which is available in our Individuals object
      // I have remove the semicolon from the above code 
      //Here in the above inside the push function we have created a new Individual object that will take preferred number and name. 
  //push Individual in our individual array ,we can also do in this way
  }


  
}

//0xd9145CCE52D386f254917e481eB44e9943F39138
```
<br><br>

It will show the following output.<br>

![U1](https://user-images.githubusercontent.com/89090776/226296418-9247522b-0ea3-4c98-b89c-471704fa12db.jpg)
Figure1:Here ```red color 1``` will show which means error occured and our code is not compiling as expected.


Here is a code that shows warning.<br>
```
// I remove the software license
pragma solidity ^0.8.7;

contract akrkSimplestorage {
  // basic data types: boolean, uint,int,address,bytes
  //uint(unsigned integer only positive),int both pos and neg
  //address is the address of the account
  //string are secretly byte objects only for text
  //bytes32 is a bytes objects whre 32 represent how many bytes we want them to be,max size is 32
  //byte objects look like 0xsdsysydggt
  //unint256 here 256 is bit (8,16,32 upto 256 we can use)
  uint256 preferredNumber;//remove public so that we don't get duplicate functions at the moment we will just get the retrieve function
   //if we have whole bunch of variables inside the contract akrkSimplestorage those actually get indexed
   //here 'uint256 preferredNumber' will get index to 'zero'
  
//Below we have created a new type in our solidity that holds both preferred number and name 
  struct Individuals{
    uint256 preferredNumber;//this get indexed to 0
    string name;// this get indexexd to 1
//whenever we have list of variables inside an object they automatically get indexed

}

  // here below we create an array of uint256 and now preferred number can be a list or array
  //uint256[] public preferredNumbersList;

//here below we want an array of Individuals we give it visibility of public and variable name individuals
  Individuals[] public individuals; //it is automatically giving a view function and it will give nothing if it is empty and in it's button the value that it wants is gonna be the index of the object
// array above is a dynamic array because size of the array is not given at it's initialization if we don't add any size it can be any size and here we gonna work with dynamic array

//pasing parameter of type uint256 and made the function public
  function store(uint256 _preferredNumber) public{
      preferredNumber = _preferredNumber;
    
  }

  function retrieve() public view returns(uint256){
    return preferredNumber;
  }

  //now we will create a function that is going to add individuals to Individual array
  function addCitizen(string memory _name, uint256 _preferredNumber) public {
      
      individuals.push(Individuals(_preferredNumber,_name));//Here we have created a push function which is available in our Individuals object
      // I have remove the semicolon from the above code 
      //Here in the above inside the push function we have created a new Individual object that will take preferred number and name. 
  //push Individual in our individual array ,we can also do in this way
  }


  
}

//0xd9145CCE52D386f254917e481eB44e9943F39138
```
It will show the following output.<br>

![u2](https://user-images.githubusercontent.com/89090776/226298356-312cd0c4-0b12-4b34-96f3-736561273097.jpg)
Figure:Here ```the yellow color 1``` shows warnings which will not stop our code from working but it is actually a good idea to check them out.<br>

<br><br>

### Learning Memory,Storage and Calldata

EVM can access and store information in the following places:<br>
1.Stack<br>
2.Memory<br>
3.Storage<br>
4.Calldata<br>
5.Code<br>
6.Logs<br>

From the above six we will focus on only Calldata,Memory and Storage.
```Calldata``` and ```Memory``` means that variables will only exist temporarily.
```Storage``` means that variables wil exits permanently

So, here in the following code:

```
//SPDX-License-Identifier: MIT
pragma solidity ^0.8.7;

contract akrkSimplestorage {
  // basic data types: boolean, uint,int,address,bytes
  //uint(unsigned integer only positive),int both pos and neg
  //address is the address of the account
  //string are secretly byte objects only for text
  //bytes32 is a bytes objects whre 32 represent how many bytes we want them to be,max size is 32
  //byte objects look like 0xsdsysydggt
  //unint256 here 256 is bit (8,16,32 upto 256 we can use)
  uint256 preferredNumber;//remove public so that we don't get duplicate functions at the moment we will just get the retrieve function
   //if we have whole bunch of variables inside the contract akrkSimplestorage those actually get indexed
   //here 'uint256 preferredNumber' will get index to 'zero'
  
//Below we have created a new type in our solidity that holds both preferred number and name 
  struct Individuals{
    uint256 preferredNumber;//this get indexed to 0
    string name;// this get indexexd to 1
//whenever we have list of variables inside an object they automatically get indexed

}

  // here below we create an array of uint256 and now preferred number can be a list or array
  //uint256[] public preferredNumbersList;

//here below we want an array of Individuals we give it visibility of public and variable name individuals
  Individuals[] public individuals; //it is automatically giving a view function and it will give nothing if it is empty and in it's button the value that it wants is gonna be the index of the object
// array above is a dynamic array because size of the array is not given at it's initialization if we don't add any size it can be any size and here we gonna work with dynamic array

//pasing parameter of type uint256 and made the function public
  function store(uint256 _preferredNumber) public{
      preferredNumber = _preferredNumber;
    
  }

  function retrieve() public view returns(uint256){
    return preferredNumber;
  }

  //now we will create a function that is going to add individuals to Individual array
  function addCitizen(string memory _name, uint256 _preferredNumber) public {
      
      individuals.push(Individuals(_preferredNumber,_name));//Here we have created a push function which is available in our Individuals object
      // I have remove the semicolon from the above code 
      //Here in the above inside the push function we have created a new Individual object that will take preferred number and name. 
  //push Individual in our individual array ,we can also do in this way
  }


  
}

//0xd9145CCE52D386f254917e481eB44e9943F39138
```

Here in ```function addCitizen(string memory _name, uint256 _preferredNumber) public{}``` function ```_name``` variable will exist temporarily during transaction.<br>
Here in the above code ```uint256 preferredNumber;``` is automatically a storage variable even though we don't specify it because it is not explictly defined in other functions.<br>


