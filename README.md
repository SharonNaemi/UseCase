# Use Case

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

This project contains a use case of a quantum workflow to show the relevance of hybrid runtimes such as [Amazon Braket Hybrid Jobs](https://docs.aws.amazon.com/braket/latest/developerguide/braket-jobs.html).
For this purpose, a quantum workflow is modeled, which realizes the VQE. Since it is a variational algorithm, which iteratively determines the solution, the loop is considered an optimization candidate in the workflow. This candidate is rewritten into a hybrid program.
This project contains the implementation of the bachelor thesis “Automated Generation of Amazon Braket Hybrid Jobs”. Quantum algorithms, which consist of classical and quantum portions, are referred to as hybrid. Thus, a repeated data transfer between classical and quantum portions takes place. Hybrid Runtimes minize these latencies by provisioning classic resources close to the QPU. The hybrid runtime programs must be generated automatically from queue-based programs, since the manual transformation is time-consuming and error-prone. Open-source projects such as the Qiskit Runtime Handler already allow the automated generation of hybrid programs. As part of this work, a concept for the automated generation of Amazon Braket Hybrid Jobs is presented, which has been prototypically implemented in the Amazon Braket Jobs Handler. 

## Disclaimer of Warranty

Unless required by applicable law or agreed to in writing, Licensor provides the Work (and each Contributor provides its Contributions) on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied, including, without limitation, any warranties or conditions of TITLE, NON-INFRINGEMENT, MERCHANTABILITY, or FITNESS FOR A PARTICULAR PURPOSE.
You are solely responsible for determining the appropriateness of using or redistributing the Work and assume any risks associated with Your exercise of permissions under this License.

## Haftungsausschluss

Dies ist ein Forschungsprototyp.
Die Haftung für entgangenen Gewinn, Produktionsausfall, Betriebsunterbrechung, entgangene Nutzungen, Verlust von Daten und Informationen, Finanzierungsaufwendungen sowie sonstige Vermögens- und Folgeschäden ist, außer in Fällen von grober Fahrlässigkeit, Vorsatz und Personenschäden, ausgeschlossen.
