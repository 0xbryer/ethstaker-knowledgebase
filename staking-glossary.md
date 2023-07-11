# Glosario de Staking

* [Archival node](staking-glossary.md#archival-node)
* [Attestation](staking-glossary.md#attestation)
* [Attestation aggregator](staking-glossary.md#attestation-aggregator)
* [Beacon chain](staking-glossary.md#beacon-chain)
* [Block](staking-glossary.md#block)
* [Block proposer](staking-glossary.md#block-proposer)
* [Block status](staking-glossary.md#block-status)
  * [Proposed](staking-glossary.md#proposed)
  * [Scheduled](staking-glossary.md#scheduled)
  * [Missed/skipped](staking-glossary.md#missedskipped)
  * [Orphaned](staking-glossary.md#orphaned)
* [Canonical chain](staking-glossary.md#canonical-chain)
* [Chain head](staking-glossary.md#chain-head)
* [Checkpoints](staking-glossary.md#checkpoints)
* [Client](staking-glossary.md#client)
* [Committees](staking-glossary.md#committees)
* [Consensus layer](staking-glossary.md#consensus-layer)
* [Deposit contract](staking-glossary.md#deposit-contract)
* [Effectiveness](staking-glossary.md#effectiveness)
* [Epoch](staking-glossary.md#epoch)
* [Execution layer](staking-glossary.md#execution-layer)
* [Finalization](staking-glossary.md#finalization)
  * [Finality issues](staking-glossary.md#finality-issues)
* [Fork](staking-glossary.md#fork)
* [Full node](staking-glossary.md#full-node)
* [Genesis block](staking-glossary.md#genesis-block)
* [Hard fork](staking-glossary.md#hard-fork)
* [Head vote](staking-glossary.md#head-vote)
* [Inactivity leak](staking-glossary.md#inactivity-leak)
* [Inclusion distance](staking-glossary.md#inclusion-distance)
* [Input data](staking-glossary.md#input-data)
* [Justification](staking-glossary.md#justification)
* [Light clients](staking-glossary.md#light-clients)
* [MEV](staking-glossary.md#mev)
* [Mempool](staking-glossary.md#mempool)
* [Node](staking-glossary.md#node)
* [Operator](staking-glossary.md#operator)
* [Participation rate](staking-glossary.md#participation-rate)
* [Peers](staking-glossary.md#peers)
* [Priority fees](staking-glossary.md#priority-fees)
* [Private key](staking-glossary.md#private-key)
* [Proof of stake (PoS)](staking-glossary.md#proof-of-stake-pos)
* [Public key](staking-glossary.md#public-key)
* [Signing](staking-glossary.md#signing)
* [Slashable offenses](staking-glossary.md#slashable-offenses)
  * [Attestation violation](staking-glossary.md#attestation-violation)
  * [Proposer violation](staking-glossary.md#proposer-violation)
* [Slasher node](staking-glossary.md#slasher-node)
* [Slot](staking-glossary.md#slot)
* [Solo staker](staking-glossary.md#solo-staker)
* [Source vote](staking-glossary.md#source-vote)
* [Staker](staking-glossary.md#staker)
* [Staking deposit CLI](staking-glossary.md#staking-deposit-cli)
* [Suggested fee recipient](staking-glossary.md#suggested-fee-recipient)
* [Sync committee](staking-glossary.md#sync-committee)
* [Target vote](staking-glossary.md#target-vote)
* [Validator](staking-glossary.md#validator)
  * [Eligible for activation & Estimated activation](staking-glossary.md#eligible-for-activation--estimated-activation)
  * [Unique index](staking-glossary.md#unique-index)
  * [Current balance & Effective balance](staking-glossary.md#current-balance--effective-balance)
* [Validator lifecycle](staking-glossary.md#validator-lifecycle)
  * [1. Deposited](staking-glossary.md#1-deposited)
  * [2. Pending](staking-glossary.md#2-pending)
  * [3. Active validator](staking-glossary.md#3-active-validator)
  * [4. Slashing validator](staking-glossary.md#4-slashing-validator)
  * [5. Exiting validator](staking-glossary.md#5-exiting-validator)
* [Validator pool](staking-glossary.md#validator-pool)
* [Validator queue](staking-glossary.md#validator-queue)
* [Validator seed phrase / mnemonic](staking-glossary.md#validator-seed-phrase--mnemonic)
* [Withdrawal address](staking-glossary.md#withdrawal-address)

***

## nodo de almacenamiento

* Almacena todo lo que se mantiene en un [#nodo-completo](staking-glossary.md#nodo-completo "mention") y crea un archivo de estados históricos.&#x20;
* Los nodos de archivo son necesarios si desea consultar algo como el saldo de una cuenta en un bloque en particular.&#x20;
* Estos datos representan unidades de terabytes (más de 20 TB para Geth), lo que hace que los nodos de archivo sean menos atractivos para la mayoría de los usuarios, pero pueden ser útiles para servicios como exploradores de bloques, proveedores de billeteras y análisis de cadenas.

La sincronización de software clientes en cualquier modo que no sea de archivo dará como resultado la eliminación de los datos extra de la cadena de bloques. Esto significa que no un nodo completo no cuenta con todos los estados históricos, pero el nodo completo puede recrearlos a pedido.

No se requiere que los nodos de archivo participen en la validación de bloques y, en teoría, pueden construirse desde cero simplemente reproduciendo los bloques desde génesis.

\*\*\*\*[**Fuente ↗**](https://ethereum.org/en/developers/docs/nodes-and-clients/#archive-node)

## atestación

Votos de [#validadores](staking-glossary.md#validadores "mention")[ ](staking-glossary.md#validadores)que confirman la validez de un [#bloque](staking-glossary.md#bloque "mention"). En momentos designados, cada validador es responsable de publicar diferentes certificaciones que declaran formalmente la visión actual de la cadena del validador, incluido el último [#checkpoints](staking-glossary.md#checkpoints "mention") finalizado y la [#cabeza-de-cadena-chain-head](staking-glossary.md#cabeza-de-cadena-chain-head "mention") actual.

Every active validator creates one attestation per [epoch](staking-glossary.md#epoch) (\~6.5 minutes), consisting of the following components:

| Component                                                                          | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Committee**                                                                      | A bitlist of validators where the position maps to the validator index in their committee. The value (0/1) indicates whether the validator signed the data (i.e. whether they are active and agree with the block proposer). |
| **Slot**                                                                           | The slot number that the attestation references.                                                                                                                                                                             |
| **Index**                                                                          | A number that identifies which committee the validator belongs to in a given slot.                                                                                                                                           |
| <p><strong>Chain head vote</strong></p><p><strong>(beacon_block_root)</strong></p> | The root hash of the block the validator sees at the head of the chain (the result of applying the fork-choice algorithm).                                                                                                   |
| **Source**                                                                         | Part of the finality vote indicating what the validators see as the most recently justified block.                                                                                                                           |
| **Target**                                                                         | Part of the finality vote indicating what the validators see as the first block in the current epoch.                                                                                                                        |
| **Signature**                                                                      | A BLS signature that aggregates the signatures of individual validators.                                                                                                                                                     |

An important component related to effectiveness is the chain head vote. This is a vote the validator makes about what it believes is the latest valid block in the chain at the time of attesting. The structure of a chain head vote consists of the following components:

* Slot - Defines _where_ the validator believes the current chain head to be.
* Hash - Defines _what_ the validator believes the current chain head to be to be.

The combination uniquely defines a point on the blockchain. By combining enough of these chain head votes the Ethereum network reaches consensus about the state of the chain.

[**Source (ethereum.org) ↗**](https://ethereum.org/en/developers/docs/consensus-mechanisms/pos/attestations/)\
[**Source (Attestant) ↗**](https://www.attestant.io/posts/defining-attestation-effectiveness/)

## Attestation aggregator

Although the data in each [attestation](staking-glossary.md#attestation) is relatively small, it mounts up quickly with tens of thousands of [validators](staking-glossary.md#validator). As this data will be stored forever on the blockchain, minimizing it is important, and this is done through a process known as attestation aggregation.

Aggregation takes multiple attestations that have all chosen to vote with the same committee, chain head vote, and finality vote, and merges them together in to a single aggregate attestation.

An aggregate attestation differs in two ways from a simple attestation. First, there are multiple validators listed. Second, the signature is an aggregate signature made from the signatures of the matching simple attestations. Aggregate attestations are very efficient to store, but introduce additional communications and computational burdens.

If every validator was required to aggregate all attestations it would quickly overload the network with the number of communications required to pass every attestation to every validator. Equally, if aggregating were purely optional then validators will not bother to waste their own resources doing so. Instead, a subset of validators is chosen by the network to carry out aggregation duties1. It is in their interest to do a good job, as aggregate attestations with higher numbers of validators are more likely to be included in the blockchain so the validator is more likely to be rewarded.

Validators that carry out this aggregation process are known as aggregators.

[_**Source ↗**_](https://www.attestant.io/posts/defining-attestation-effectiveness/)

## beacon chain

Una parte importante del trabajo de la beacon chain es almacenar y administrar el registro de [#validadores](staking-glossary.md#validadores "mention") - el conjunto de participantes responsables de ejecutar el sistema Ethereum [#proof-of-stake-pos](staking-glossary.md#proof-of-stake-pos "mention").

Este registro se utiliza para:

* Assigns validators their duties.
* Asigna a los validadores sus funciones.
* Finaliza los [#checkpoints](staking-glossary.md#checkpoints "mention").&#x20;
* Realice una generación de números aleatorios (RNG) a nivel de protocolo.&#x20;
* Avanza la [#beacon-chain](staking-glossary.md#beacon-chain "mention"). Vote en la [#chain-head](staking-glossary.md#chain-head "mention") elegir el fork.

[_**Fuente ↗**_](https://notes.ethereum.org/@djrtwo/Bkn3zpwxB#High-level-overview)

## bloque

Un bloque es una unidad de información agrupada que incluye una lista ordenada de transacciones e información relacionada con el consenso. Los bloques son propuestos por validadores de [Proof of Stake (PoS)](staking-glossary.md#proof-of-stake-pos)), momento en el que se comparten en toda la red peer-to-peer, donde todos los demás nodos pueden verificarlos fácilmente de forma independiente. Las reglas de consenso rigen qué contenidos de un bloque se consideran válidos, y la red ignora cualquier bloque no válido. El orden de estos bloques y las transacciones en ellos crean una cadena determinista de eventos cuyo final representa el estado actual de la red.

## Block proposer

A chosen [validator](staking-glossary.md#validator) by the [Beacon Chain](staking-glossary.md#beacon-chain) to propose the next [block](staking-glossary.md#block). There can only be one valid block per [slot](staking-glossary.md#slots).

## Estado del Bloque

### Propuesto (Proposed)

El bloque fue propuesto por un validador.

### Programado (Scheduled)

Los validadores están enviando datos actualmente.

### Perdido/omitido (Missed/skipped)

El proponente no propuso el bloque dentro del plazo dado, por lo que el bloque se perdió/se saltó.

### Huérfano (Orphaned)

Para entender esto, miremos el diagrama debajo de "1, 2, 3, ..., 9" representan los slots (ranuras).

1. El validador en el slot 1 propone el bloque "a".
2. El validador en el slot 2 propone "b".
3. El slot 4 se está omitiendo porque el validador no propuso un bloque (por ejemplo, fuera de línea).
4. En el slot 5/6 se produce una bifurcación: el validador (5) propone un bloque, pero el validador (6) no recibe estos datos (por ejemplo, el bloque no los alcanzó lo suficientemente rápido). Por lo tanto, Validator(6) propone su bloque con la información más reciente que ve de validator(3).
5. La [regla de elección de fork (bifurcación) ↗](https://notes.ethereum.org/@vbuterin/rkhCgQteN?type=view#LMD-GHOST-fork-choice-rule)  es la clave aquí: decide cuál de las cadenas disponibles es la canónica.

## cadena canónica

La cadena canónica es la cadena que se acuerda que es la cadena "principal" y no un [fork](staking-glossary.md#fork).

## cabeza de cadena

El último bloque recibido por un validador. Esto no significa necesariamente que sea la cabeza de la [#cadena-canonica](staking-glossary.md#cadena-canonica "mention").

## checkpoints

La [#beacon-chain](staking-glossary.md#beacon-chain "mention") tiene un tempo dividido en [#slot](staking-glossary.md#slot "mention")s (12 segundos) y [#epoca](staking-glossary.md#epoca "mention")s (32 slots). El primer slot en cada época es un checkpoint. Cuando una gran mayoría de validadores [da fe ](staking-glossary.md#atestacion)del vínculo entre dos checkpoints, se pueden [justificar ](staking-glossary.md#justificacion)y luego, cuando se justifica otro checkpoint encima, se pueden [finalizar](staking-glossary.md#finalizacion).

## software cliente

Una implementación del software Ethereum que verifica las transacciones en un bloque. Estos pueden ser [clientes de capa de consenso](https://ethereum.org/en/developers/docs/nodes-and-clients/#consensus-clients)  o [clientes de capa de ejecución](https://ethereum.org/en/developers/docs/nodes-and-clients/#execution-clients). Cada validador necesita tanto un cliente de capa de ejecución como un cliente de capa de consenso.

## comités

Un grupo de al menos 128 [#validadores](staking-glossary.md#validadores "mention") asignados para validar bloques en cada [#slot](staking-glossary.md#slot "mention"). Uno de los validadores del comité es el agregador, responsable de agregar las firmas de todos los demás validadores del comité que acuerdan una [#atestacion](staking-glossary.md#atestacion "mention"). No debe confundirse con los [#comite-de-sincronizacion](staking-glossary.md#comite-de-sincronizacion "mention").

## capa de consenso

La capa de consenso de Ethereum es la red de [consensus-clients.md](validator-clients/consensus-clients.md "mention").

## contrato de depósito

El contrato de depósito es la puerta de entrada a Ethereum [#proof-of-stake-pos](staking-glossary.md#proof-of-stake-pos "mention") y se administra a través de un **contrato inteligente** en Ethereum. El contrato inteligente acepta cualquier transacción con una cantidad mínima de 1 ETH y [#datos-de-entrada](staking-glossary.md#datos-de-entrada "mention") válidos. Los nodos de [#beacon-chain](staking-glossary.md#beacon-chain "mention") escuchan el contrato de depósito y usan los datos de entrada para acreditar cada validador.&#x20;

[_Más información sobre el contrato de depósito_](para-empezar/deposit-process.md)

## efectividad

El tiempo medio que tardan las certificaciones de un validador en incluirse en la cadena.

[_Revisa nuestra página sobre validator effectiveness_ ](validator-clients/validator-effectiveness.md)

## época

**1 época = 32** [**slots**](staking-glossary.md#slot)\
Representa el número de 32 slots (12 segundos) y tarda aproximadamente **6,4 minutos**. Las épocas juegan un papel importante cuando se trata de la cola y la finalidad del validador.

epresents the number of 32 slots (12 seconds) and takes approximately **6.4 minutes.** Epochs play an important role when it comes to the [validator queue](staking-glossary.md#validator-queue) and [finality](staking-glossary.md#finalization).

## capa de ejecución

La capa de ejecución de Ethereum es la red de [clientes de ejecución](validator-clients/execution-clients.md).&#x20;

## finalización

En Ethereum [#proof-of-stake-pos](staking-glossary.md#proof-of-stake-pos "mention") al menos dos tercios de los validadores deben ser honestos, por lo tanto, si hay dos [#epoca](staking-glossary.md#epoca "mention") en competencia y un tercio de los [#validadores](staking-glossary.md#validadores "mention") deciden ser maliciosos, recibirán una penalización. Los validadores honestos serán recompensados.

Para determinar si se ha finalizado una época, los validadores deben ponerse de acuerdo sobre las últimas dos épocas seguidas, luego todas las épocas anteriores se pueden considerar finalizadas.

### problemas de finalidad

Si hay menos del 66,6% del total de votos posibles (la [#tasa-de-participacion](staking-glossary.md#tasa-de-participacion "mention")) en una época específica, la época no se puede justificar. Como se mencionó en "Finalización", se requieren tres épocas consecutivas justificadas para alcanzar la finalización. Mientras la cadena no pueda alcanzar este estado, tiene problemas de finalidad.

&#x20;there are less than 66.6% of the total possible votes (the [participation rate](staking-glossary.md#participation-rate)) in a specific epoch, the epoch cannot be [justified](staking-glossary.md#justification). As mentioned in "[Finalization](staking-glossary.md#finalization)", three justified epochs in a row are required to reach finality. As long as the chain cannot reach this state it has finality issues.

During finality issues, the validator [entry queue](staking-glossary.md#validator-queue) will be halted and new validators will not be able to join the network, however, inactive validators with less than 16 ETH balance will be exited from the network. This leads to more stability in the network and a higher participation rate, allowing the chain to eventually finalize.

## fork

Un cambio en el protocolo que provoca la creación de una cadena alternativa o una divergencia temporal en dos posibles rutas de bloques. Ver también [#hard-fork](staking-glossary.md#hard-fork "mention")

## nodo completo

Almacena y mantiene los datos completos de la cadena de bloques en el disco. Provee datos de blockchain a solicitud y ayuda a respaldar la red participando en la validación de bloques y verificando todos los bloques y estados. Todos los estados se pueden derivar de un nodo completo.

[**Fuente ↗**](https://www.quicknode.com/guides/infrastructure/ethereum-full-node-vs-archive-node)

## bloque Génesis

El primer bloque en una cadena de bloques, utilizado para inicializar una red en particular y su criptomoneda.

## hard fork

Se produce un hard fork  cuando se envía una actualización a la red Ethereum y la nueva versión del software se bifurca de la versión anterior. Por lo general, requiere que los operadores actualicen su software de validación para permanecer en el lado correcto del fork. Ver también  [#fork](staking-glossary.md#fork "mention")

## Head voteVoto principal

The validator has made a timely vote for the correct [head block](staking-glossary.md#chain-head).

## Inactivity leak

If the Beacon Chain has gone more than four [epochs](staking-glossary.md#epoch) without [finalizing](staking-glossary.md#finalization), an emergency protocol called the "inactivity leak" is activated. The ultimate aim of the inactivity leak is to create the conditions required for the chain to recover finality. Finality requires a 2/3 majority of the total staked ether to agree on source and target checkpoints. If validators representing more than 1/3 of the total validators go offline or fail to submit correct [attestations](staking-glossary.md#attestation) then it is not possible for a 2/3 supermajority to finalize checkpoints. The inactivity leak lets the stake belonging to the inactive validators gradually bleed away until they control less than 1/3 of the total stake, allowing the remaining active validators finalize the chain. However large the pool of inactive validators, the remaining active validators will eventually control >2/3 of the stake. The loss of stake is a strong incentive for inactive validators to reactivate as soon as possible!

## Inclusion distance

The inclusion distance of a [slot](staking-glossary.md#slot) is the difference between the slot in which an [attestation](staking-glossary.md#attestation) is made and the lowest slot number of the block in which the attestation is included. For example, an attestation made in slot _s_ and included in the block at slot _s + 1_ has an inclusion distance of _1_. If instead the attestation was included in the block at slot _s + 5_ the inclusion distance would be _5_.

The value of an attestation to the Ethereum network is dependent on its inclusion distance, with a low inclusion distance being preferable. This is because the sooner the information is presented to the network, the more useful it is.

To reflect the relative value of an attestation, the reward given to a validator for attesting is scaled according to the inclusion distance. Specifically, the reward is multiplied by _1/d_, where _d_ is the inclusion distance.

<figure><img src=".gitbook/assets/InclusionDistance.png" alt="Attestation Reward Inclusion Distance Distribution"><figcaption></figcaption></figure>

## datos de entrada

Los datos de entrada, también llamados **datos de depósito**, son una secuencia de 842 caracteres generada por el usuario. Representa la [#llave-publica](staking-glossary.md#llave-publica "mention") y la llave pública de retiro, que fueron firmadas con la [#llave-privada](staking-glossary.md#llave-privada "mention") del validador. Los datos de entrada deben agregarse a la transacción del [#contrato-de-deposito](staking-glossary.md#contrato-de-deposito "mention") para que la [#beacon-chain](staking-glossary.md#beacon-chain "mention") los identifique.

[_Más información sobre el contrato de depósito_](para-empezar/deposit-process.md)

## justificación

El 66,6% del total de validadores necesitan dar fe a favor de la inclusión de un bloque en la [#cadena-canonica](staking-glossary.md#cadena-canonica "mention"). Esta condición actualiza el bloque a "justificado". Es poco probable que los bloques justificados se reviertan, pero pueden hacerlo bajo ciertas condiciones.&#x20;

Cuando se justifica otro bloque encima de un bloque justificado, se actualiza a "finalizado". Finalizar un bloque es un compromiso de incluir el bloque en la cadena canónica.&#x20;

[_Más información sobre la justificación ↗_](https://ethereum.org/en/developers/docs/consensus-mechanisms/pos/gasper/)

## clientes ligeros

Un cliente de Ethereum que no almacena una copia local de la cadena de bloques ni valida bloques y transacciones. Ofrece las funciones de una billetera y puede crear y transmitir transacciones.

## MEV

MEV o "valor extraíble máximo", es un tema controversial. Los operadores de nodos pueden extraer MEV aceptando bloques creados por "buscadores", a través de un pequeño programa secundario llamado  "[mev-boost ↗](https://ethresear.ch/t/mev-boost-merge-ready-flashbots-architecture/11177)". En este caso, el cliente de la capa de consenso, como Nimbus, Teku, etc., cuando se le solicite obtener un bloque para proponer, obtendrá bloques de los relés MEV a través de mev-boost y del cliente de la capa de ejecución, como Besu, Geth, etc. y luego elija el bloque del relé que mejor pague. Actualmente, la capa de ejecución no comunica su pago esperado y solo se elegiría cuando el relevo no ofrezca ningún bloque. Para esto, se debe confiar en que el relé entregará bloques válidos. Las recompensas de MEV se pagan a la misma dirección del destinatario de la tarifa sugerida que las tarifas prioritarias.

Las recompensas de MEV se pagan a la misma dirección del destinatario de la tarifa sugerida que las tarifas prioritarias.

ewards from MEV are paid to the same [suggested fee recipient](staking-glossary.md#suggested-fee-recipient) address as [priority fees](staking-glossary.md#priority-fees).

[_**Source ↗**_](https://ethereum.org/en/developers/docs/mev/)

## mempool

Cuando un nodo Ethereum recibe una transacción, no se agrega instantáneamente a un bloque. La transacción se lleva a cabo en un área de espera o una zona de amortiguamiento.

La transacción pasa por una serie de niveles de verificación, como comprobar si la salida es mayor que la entrada, si la firma es válida o no, etc., y luego solo se agrega a un bloque. La transacción no se agrega a un bloque si falla alguna de estas validaciones. El papel de un mempool surge mientras una transacción pasa por estos controles. Simplemente se mantiene en esta sala de espera o en un mempool. Tan pronto como se confirma la transacción, se elimina del mempool y se agrega a un bloque. Mempool no es una referencia maestra compartida universalmente por todos los nodos. No hay un mempool "único". Esto significa que cada nodo configura sus propias reglas para el mempool del nodo. De hecho, un nodo puede ser el primero en recibir una transacción, pero es posible que no haya propagado la transacción al resto de la red.

[**Fuente ↗**](https://www.geeksforgeeks.org/what-is-ethereum-mempool/)

## nodo

Una instancia de software de cliente de Ethereum que esté conectada a otras computadoras que también ejecuten software de Ethereum, formando una red. Un nodo no necesita necesariamente un validador, pero un validador requiere un nodo. Ejecutar un nodo por sí solo no genera ningún ingreso, pero contribuye a la solidez de la red.

## operador

Una persona que mantiene un validador.

## tasa de participación

La tasa de participación es el porcentaje de validadores que están en línea y realizando sus funciones.

Si el conjunto de validadores es de 1000 validadores y 250 validadores están fuera de línea o rara vez hacen propuestas o certificaciones, entonces se podría estimar que la tasa de participación es del 75 %.

[**Fuente ↗**](https://ethereum.stackexchange.com/questions/87503)

## peers

Otros nodos que ejecutan clientes de Ethereum que se conectan entre sí a través de una red de igual a igual (peer to peer). La comunicación entre peers es la forma en que la red Ethereum permanece descentralizada ya que no hay un punto único de falla.

## Priority fees

Almost all transaction on Ethereum set a [priority fee ↗](https://ethereum.org/en/developers/docs/gas/#priority-fee) to incentivize [block proposers](staking-glossary.md#block-proposer) to include the transaction as a higher priority than others. The higher the fee relative to other transactions currently waiting in the [mempool](staking-glossary.md#mempool) This fee is paid to the block proposer. All of the priority fees in a block are aggregated and paid in a single state change directly to the [suggested fee recipient](staking-glossary.md#suggested-fee-recipient) set by the block proposer. This address could be a hardware wallet, a software wallet, or even a multi-sig contract.

## llave privada

(Private Key) Un número secreto que permite a los usuarios de Ethereum demostrar la propiedad de una cuenta o contratos mediante la producción de una firma digital.

## proof of stake (PoS)

Un método por el cual un protocolo de cadena de bloques de criptomonedas tiene como objetivo lograr un consenso distribuido. PoS pide a los usuarios que demuestren la propiedad de una cierta cantidad de criptomonedas (su "participación" en la red) para poder participar en la validación de transacciones.

## llave publica

Un número, derivado a través de una función unidireccional de una [#llave-privada](staking-glossary.md#llave-privada "mention"), que puede ser compartido públicamente y utilizado por cualquier persona para verificar una firma digital realizada con la clave privada correspondiente.

## firmar

Demostrar criptográficamente que un mensaje o transacción fue aprobado por el titular de una  [#llave-privada](staking-glossary.md#llave-privada "mention").

## Slashable offenses

If your validator commits a slashable offense it will be force exited from the validator pool and will have ETH deducted depending on the circumstances of the event. Typically, this will be 1-2 ETH but could be [significantly more ↗](https://ethereum.org/en/developers/docs/consensus-mechanisms/pos/rewards-and-penalties/#slashing).

This is not something to be overly worried about, there are [simple steps](help/slashing-explained.md) you can take to make sure that you don't invoke a slashing event.

There are three ways a validator can be slashed, all of which amount to the dishonest proposal or attestation of blocks.

### Attestation violation

* **Double voting**: Signing two different [attestations](staking-glossary.md#attestation) in one [epoch](staking-glossary.md#epoch).
* **Surround votes**: Attesting to a block that "surrounds" another one (effectively changing history).

### Proposer violation

* **Double block proposal**: [Proposing](staking-glossary.md#block-proposer) and [signing](staking-glossary.md#signing) two different [blocks](staking-glossary.md#block) for the same [slot](staking-glossary.md#slot).

## Slasher node

The [**slasher**](https://github.com/Buttaa/ethstaker/blob/main/slasher.md) **is its own entity** but requires a beacon-node to receive [attestations](https://kb.beaconcha.in/glossary#attestation). To find malicious activity by validators, the slashers iterates through all received attestations until a **slashable offense** has been found. Found slashings are broadcasted to the network and the next [block proposer](staking-glossary.md#block-proposer) adds the proof to the block. The block proposer receives a reward for slashing the malicious validator. However, the whistleblower (Slasher) does not receive a reward.

## slot

**32 slots = 1** [#epoca](staking-glossary.md#epoca "mention")\
Un período de tiempo de 12 segundos en el que un validador elegido al azar tiene tiempo para proponer un bloque. El número total de validadores se divide en [#committees](staking-glossary.md#committees "mention") y uno o más comités individuales son responsables de dar fe de cada puesto. Se elegirá un validador del comité para que sea el agregador, mientras que los otros 127 validadores dan fe. Después de cada época, los validadores se mezclan y fusionan en nuevos comités. Cada espacio puede tener o no un bloque, ya que un validador podría perder su propuesta (por ejemplo, puede estar desconectado o enviar su bloque demasiado tarde). Hay un mínimo de 128 validadores por comité.

A time period of **12 seconds** in which a randomly chosen validator has time to propose a block. The total number of validators is split up in [committees](staking-glossary.md#committees) and one or more individual committees are responsible to attest to each slot. One validator from the committee will be chosen to be the aggregator, while the other 127 validators are attesting. After each Epoch, the validators are mixed and merged to new committees. Each slot may or may not have a block in it as a validatory could miss their proposal (e.g. they may be offline or submit their block too late). There is a minimum of 128 validators per committee.

## staker individual

Un operador que ejecuta un validador en la red Ethereum sin un protocolo entre su validador y [#beacon-chain](staking-glossary.md#beacon-chain "mention")

## voto de origen

El validador ha votado oportunamente por el origen correcto del [checkpoint](staking-glossary.md#checkpoint).

## staker

Alguien que ha depositado ETH en un validador para asegurar la red. Puede ser alguien que ejecuta un validador (un operador) o alguien que depositó su ETH en un grupo, donde otra persona es el operador del validador.

## staking CLI

Una herramienta de línea de comandos utilizada para generar claves de validación y depositar archivos de datos.

* [https://github.com/ethereum/staking-deposit-cli](https://github.com/ethereum/staking-deposit-cli)

## Suggested fee recipient

The fee recipient is an Ethereum address nominated by a [Beacon Chain](staking-glossary.md#beacon-chain) validator to receive tips from user transactions and [MEV](staking-glossary.md#mev).

## comité de sincronización

Un comité de sincronización es un grupo de [#validadores](staking-glossary.md#validadores "mention")seleccionados al azar que se actualizan cada \~27 horas. Su propósito es agregar sus [#firmar](staking-glossary.md#firmar "mention") a encabezados de bloque válidos. Los comités de sincronización permiten a los [#clientes-ligeros](staking-glossary.md#clientes-ligeros "mention")  realizar un seguimiento de la [#chain-head](staking-glossary.md#chain-head "mention") jefe de la cadena de bloques sin necesidad de acceder a todo el conjunto de validadores. Ocurre cada 2 años en promedio, sin embargo, puede haber "períodos secos" varias veces más largos que el promedio sin que se dé uno. Entonces, si su validador es seleccionado... ¡felicidades! 🥳

A sync committee is a randomly selected group of [validators](staking-glossary.md#validator) that refresh every \~27 hours. Their purpose is to add their [signatures](staking-glossary.md#signing) to valid block headers. Sync committees allow [light clients](staking-glossary.md#light-clients) to keep track of the head of the blockchain without needing to access the entire validator set. Occurs every 2 years on average, however, there can be "dry spells" multiple times longer than the average without being given one. So if your validator is selected... congratulations! 🥳

## voto destino

El validador ha votado a tiempo por el destino correcto del [checkpoint](staking-glossary.md#checkpoints).

## validadores

Un nodo en un sistema de [#proof-of-stake-pos](staking-glossary.md#proof-of-stake-pos "mention") responsable de almacenar datos, procesar transacciones y agregar nuevos bloques a la cadena de bloques. Para activar el software de validación, debe poder aportar 32 ETH. El trabajo de los validadores es proponer bloques y firmar atestaciones. Tiene que estar en línea durante al menos el 50% del tiempo para tener retornos positivos. Un validador lo ejecuta un operador (un ser humano), en el hardware (una computadora) y se empareja con un nodo (muchos miles de validadores pueden ejecutarse en un nodo)

### elegible para activación y activación estimada

Se refiere a validadores pendientes. El depósito ha sido reconocido por [#beacon-chain](staking-glossary.md#beacon-chain "mention") en la marca de tiempo de "Elegible para activación". Si hay una cola de [validadores pendientes ↗](https://www.beaconcha.in/validators), se calcula una marca de tiempo estimada para la activación.

### índice único

Cada validador recibe un índice único en función de cuándo se agregan desde el [validator queue](staking-glossary.md#validator-queue).

### saldo actual y saldo efectivo

El saldo actual es la cantidad de ETH que tiene el validador a partir de ahora. El saldo efectivo representa un valor calculado por el saldo actual. Se utiliza para determinar el tamaño de una recompensa o penalización que recibe un validador. El saldo efectivo nunca puede ser superior a 32 ETH.&#x20;

Para aumentar el saldo efectivo, el validador requiere "saldo efectivo + 1.25 ETH". En otras palabras, si el saldo efectivo es de 20 ETH, se requiere un saldo actual de 21,25 ETH para tener un saldo efectivo de 21 ETH. El saldo efectivo se ajustará una vez que caiga 0,25 por debajo del umbral, como se ve en los ejemplos anteriores.

Aquí hay ejemplos de cómo cambia el saldo efectivo:

* Si el saldo actual es 32,00 ETH, el saldo efectivo es 32,00 ETH.
* Si el saldo actual se redujo de 22 ETH a 21,76 ETH, el saldo efectivo será de **22,00 ETH**.
* Si el saldo actual aumenta a 22,25 **y** el saldo efectivo es de 21 ETH, el saldo efectivo aumentará a 22 ETH.

## Validator lifecycle

#### 1. Deposited

32 ETH has been deposited to the ETH1 deposit-contract and this state will be kept for around 7 hours. This offers security in case the Ethereum chain gets attacked.

#### 2. Pending

Waiting for activation on the [Beacon Chain](staking-glossary.md#beacon-chain).

Before validators enter the [validator queue](staking-glossary.md#validator-queue), they need to be voted in by other active validators. This occurs every 4 hours.

#### 3. Active validator

Currently attesting and proposing blocks.

The validator will stay active until:

* Its balance drops below 16 ETH (ejected).
* Voluntary exit.
* It gets slashed.

#### 4. Slashing validator

The Validator has been malicious and will be slashed and kicked out of the system.

> A _**Penalty**_ is a negative reward (e.g. for going offline).\
> A _**Slashing**_ is a large penalty (≥ 1/32 of balance at stake) and a forceful exit ... **. - Justin Drake**

#### 5. Exiting validator

* **Ejected**: The validator balance fell below a threshold and was kicked out by the network.
* **Exited**: Voluntary exit, the withdrawal key holder has the ability to **withdraw** the current balance of the corresponding validator balance.

## grupo de validadores

El número de validadores actualmente activos que aseguran la red Ethereum. El grupo de validadores actual se puede [ver aquí ↗](https://beaconcha.in/validators).

## cola de validación

La cola de validación es una cola de primero en entrar, primero en salir para activar y salir de los validadores en el [#beacon-chain](staking-glossary.md#beacon-chain "mention").

* Hasta 327680 validadores activos en la red, se pueden activar 4 validadores por [#epoca](staking-glossary.md#epoca "mention"). Por cada (4 \* 16384) = **65536** validadores activos, la tasa de activación del validador aumenta en uno.
* 5 validadores por época requiere 327680 validadores activos, lo que permite 1125 validadores por día.
* 6 validadores por época requiere 393216 validadores activos, lo que permite 1350 validadores por día.
* 7 validadores por época requiere 458752 validadores activos, lo que permite 1575 validadores por día.
* 8 validadores por época requiere 524288 validadores activos, lo que permite 1800 validadores por día.
* 9 validadores por época requiere 589824 validadores activos, lo que permite 2025 validadores por día.
* 10 validadores por época requiere 655360 validadores activos, lo que permite 2200 validadores por día.
* La cantidad de activaciones escala con la cantidad de validadores activos y el límite es el conjunto de validadores activos dividido por 64.

La salida de validadores funciona de la misma manera, con la cantidad de validadores que pueden salir de Beacon Chain por tasa diaria limitada para preservar la estabilidad de la red.

## frase semilla / mnemotécnico

La frase semilla o mnemotécnica es un conjunto de palabras (generalmente de 12, 18 o 24 palabras) que se utiliza para generar sus claves de validación. Su mnemónico es la copia de seguridad de sus claves de validación y será la ÚNICA forma de retirar su ETH cuando llegue el momento y nadie puede ayudarlo a recuperar su mnemónico si lo pierde.

## dirección de retiro

Una dirección que se puede configurar opcionalmente al crear una clave de validación que se usará para retirar ETH apostado. Si esta dirección no se configura en el momento de la creación de la clave, se puede configurar en el momento del retiro. Para obtener más información sobre cómo configurar la dirección de retiro en la creación de la clave, consulte nuestra respuesta a las [preguntas frecuentes](faq.md).
