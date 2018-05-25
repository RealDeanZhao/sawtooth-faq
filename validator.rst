* Is there a simple example to show how to run Sawtooth
See these instructions to install and use Sawtooth with Docker, Ubuntu Linux, or AWS:
https://sawtooth.hyperledger.org/docs/core/nightly/master/app_developers_guide/installing_sawtooth.html

* Is there an example for a multiple node Sawtooth Network?
See these instructions for setting up a 5-node Sawtooth Network with Poet Simulator Consensus using Docker:
https://sawtooth.hyperledger.org/docs/core/nightly/master/app_developers_guide/creating_sawtooth_network.htmlow do I add a node to a Sawtooth Network?
* How do I add a node to a Sawtooth Network?

See
https://sawtooth.hyperledger.org/docs/core/nightly/master/app_developers_guide/creating_sawtooth_network.html#ubuntu-add-a-node-to-the-single-node-environment

* How do I verify the Validator is running and reachable?
Run the following command from the Validator Docker container or from where the Validator is running:
        curl http://localhost:8008/blocks
This verifies the REST API is available.
From the Client Docker container run this:
        curl http://rest-api:8008/blocks

You should see a JSON response similar to this:
{
  "data": [
    {
      "batches": [
        {
          "header": {
            "signer_public_key": . . .

* Do all validators need to run the same transaction processors?

Yes.  All validators must run all of the same transaction processors that are
on the network. If a validator receives a transaction that it does not have a
transaction processor for, the validator will wait until a transaction processor
connects that can handle that transaction. That validator would fall behind the
rest on the network while it waits. You can also limit which transactions are
accepted on the network with the `sawtooth.validator.transaction_families`
setting.  If that setting is not set, all transaction would be accepted.

* I set sawtooth.validator.transaction_families as follows (from the documentation) but it's ignored:
sawset proposal create sawtooth.validator.transaction_families='[{"family": "intkey", "version": "1.0"}, {"family":"sawtooth_settings", "version":"1.0"}]'

The sawtooth.validator.transaction_families setting is ignored using dev-mode consensus and does not need to be set.