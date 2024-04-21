`Missing Event Emission in setFee Function`

https://github.com/code-423n4/2024-04-dyad/blob/49fb7174576e5147dc73d3222d16954aa641a2e0/src/periphery/Payments.sol#L32

The setFee function lacks event emission after updating the fee value. This omission reduces transparency regarding fee modifications within the contract. Implementing event emission enhances contract transparency and auditability, ensuring that fee changes are recorded and accessible to users and external systems.

It is recommended to implement event emission within the setFee function immediately after updating the fee value. Emitting an event (FeeSet or similar) provides transparent and auditable records of fee modifications, enhancing user trust and facilitating contract monitoring.

function setFee(uint _fee) external onlyOwner {
    fee = _fee;
    emit FeeSet(_fee);
}



`Ignoring Return Value in asset.approve Function Call`

https://github.com/code-423n4/2024-04-dyad/blob/49fb7174576e5147dc73d3222d16954aa641a2e0/src/periphery/Payments.sol#L75

 During the audit, it was observed that the `asset.approve` function call in the `_deposit` function is not checking its return value. This omission could lead to unexpected behavior if the approval fails for any reason.
If the approval process fails, the contract may not be aware of it, leading to potential security vulnerabilities.
Failure to handle the approval process correctly may result in unexpected behavior or leave the contract in an unintended state.

Update the _deposit function to check the return value of the asset.approve function call.
If the approval fails, revert the transaction or take appropriate corrective actions to ensure the contract's integrity and security.

function _deposit(
    uint id,
    address vault,
    uint amount
) internal {
    ERC20 asset = Vault(vault).asset();

    uint feeAmount = amount.mulWadDown(fee);
    asset.safeTransfer(feeRecipient, feeAmount);

    uint netAmount = amount - feeAmount;
   ` require(asset.approve(address(vaultManager), netAmount), "Approval failed");`

    vaultManager.deposit(id, vault, netAmount);
}
