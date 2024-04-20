Before deploying your contract, activate the optimizer when compiling using “solc --optimize --bin sourceFile.sol”. By default, the optimizer will optimize the contract assuming it is called 200 times across its lifetime. If you want the initial contract deployment to be cheaper and the later function executions to be more expensive, set it to “ --optimize-runs=1”. Conversely, if you expect many transactions and do not care for higher deployment cost and output size, set “--optimize-runs” to a high number.

    # See more config options https://github.com/foundry- 
    rs/foundry/tree/master/config

    [profile.default]
    src = 'src'
    out = 'out'
    libs = ['lib']

    # viaIR = true 
    optimizer_runs = 1_000_000

Please visit the following site for further information:

https://docs.soliditylang.org/en/v0.5.4/using-the-compiler.html#using-the-commandline-compiler