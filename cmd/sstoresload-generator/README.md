## SSTORE and SLOAD fuzzing

This implements a fuzzer targeting SSTORE and SLOAD, to test out the implementations
of EIP-2200 (EIP-1283). 


### Fuzzing scheme

The fuzzer create a set of accounts (10) (`[addrs]`), and initializes each with random code. 
The code generated by `randcode` will randomly select from the following actions

	// 30% sstore,
	// 30% sload,
	// 20% call of some type (CALL, CALLCODE, STATIC etc), to one of addrs
	// 5% create, 5% create2,
	// 5% return, 5% revert

A `CREATE/CREATE2` + `CALL(addr)`, will have init-code that does
   
    // 40% chance of sstore,
    // 40% chance of sload
    // 20% chance of nothing more

and then deploys bytecode generated as outlined above. 
   

The idea is to set/reset slots from various contexts, newly created and not, reverted and not. 




