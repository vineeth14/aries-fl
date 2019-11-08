# Distributed Deep-learning DID-acts

This repo has been forked from Hyperledger Aries Cloud agent [link](https://github.com/hyperledger/aries-cloudagent-python) provided by British Columbia Government.

We have created a set of agents that can be run using docker to experiment with a federated deep learning scenario using didCOMM to pass secure messages between the participants - e.g. the ML model parameters. Furthermore the scenario explores using credentials so that participants can verify that who they are communicating with. In the example this is verifying a hospital is indeed a hospital and a researcher has been accredited by a regulator. However the credentials abnd issuers within this use case could be adapted to any ecosystem.

The agents connect, by default, to the BC government development instance of Hyperledger Indy ledger [link](http://dev.bcovrin.vonx.io).



# Guide

![Full Aries Scenario](./figures/initialidea.png)

To run the scenario:

```
git clone https://github.com/blockpass-identity-lab/diffusion2019.git

cd demo
```

## Hospital gets verified by the NHS Trust.

![Trust Issues to Hospital](./figures/Trust_to_Hospital.png)

1) Start the NHS Trusted agent.
```
./run_demo nhsheadoffice
```
2) Start each of the hospitals in separate terminals.
```
./run_demo hospital1(2,3)
```
3) Copy NHS's invitation URL into the hospitals terminal to establish pairwise DID connection.

4) Trust requests proof of hospitals name (Self attested)

5) NHS Trust issue verified hospital credential to the Hospital.

6) Repeat for each hospital

## The Researcher gets accredited by the regulatory authority.

![Researcher accreditation](./figures/regulator_to_coordinator.png)

7) Start the Coordinator.
```
./run_demo coordinator
```

8) Start the regulator.

```
./run_demo regulator
```

9) Follow the on-screen menu on the coordinator (3) to input connection url from the regulator.

10) Follow the on-screen menu to Issue a credential from the Regulator to the Coordinator.


## The researcher validates the hospital's credential. The hospital validates the researcher's accreditation. The training procedure starts.

![Researcher and hospital verify respective credentials](./figures/trusted_connection.png)

11) Follow the on-screen menu on the Coordinator (2) to create New Invitation for the hospital.

12) Follow the on-screen menu in the hospital terminal to accept the new invitation link from the coordinator, and connect to it.

13) Follow the on-screen menu (1) so the coordinator can check the hospital's credentials. If proof is valid, the coordinator adds this hospital to the list of the trusted connections.

14) Follow the on-screen menu (3) in the hospital to request proof that the coordinator has been regulated. If so add to list of trusted connection.

15) Either add another trusted connection between a new hospital and current researcher
 
or..

16) In the coordinator terminal initiate training process by accepting the model from the coordinator, trains the model, and sends back the updated model (updated model parameters) to the coordinator. Afterwards, coordinator sends the new updated model to the next hospital to continue the training until the full training procedure has been completed.

![Researcher coordinates federated learning](./figures/federated_learning.png)

# The Ledger that has been used:

LEDGER_URL=http://dev.bcovrin.vonx.io ./run_demo $AGENT_NAME

# Created by

    Will Abramson
    Adam James Hall
    Pavlos Papadopoulos
