---
title: JAM - Transforming Math Formulas into Code 
description: How we can read the Graypaper and understand it by coding
duration: 30+ mins
---

## What is this talk NOT About?

* What is JAM 🚫 
* Why JAM is useful 🚫
* How JAM is different from Polkadot 🚫

---

## What is this talk About?

* Hands-on approach ✅
* Read (and understand) math formulas ✅
* Implement JAM in actual code ✅

---

## JAM Crypto Innovations

<img width="1000px" src="../../assets/img/7-Polkadot/jam-comparison.png" />

---

## JAM Crypto Innovations

<!--  .slide: data-visibility="hidden" -->

 - Polkadot Virtual Machine (PVM) - RISC-V
 - Erasure Coding DA
 - VRF Ring Signatures / Bandersnatch
 - In-core + on-chain 
 - Parallel Execution
     - Each Core runs different computing jobs
     - State components updated in parallel
 - Safrole and Grandpa - less forks

---

# Formal Specification

---

## PVM 

<img width="1000px" src="../../assets/img/7-Polkadot/pvm-formula.png" />

---

## Erasure Coding

<img width="1000px" src="../../assets/img/7-Polkadot/erasure-coding.jpg" />

---

## Bandersnatch


<img width="1000px" src="../../assets/img/7-Polkadot/bandersnatch.png" />

---

## Block Structure

<img width="400px" src="../../assets/img/7-Polkadot/jam-block.png" />

```rust
struct Block {
    header: Header,
    extrinsic: Extrinsic,
}
```

---

## Extrinsic Structure

<img width="400px" src="../../assets/img/7-Polkadot/jam-extrinsics.png" />

```rust
struct Extrinsic {
    tickets: Vec<Ticket>,
    disputes: Disputes,
    preimages: Vec<Preimage>,
    assurances: Vec<Assurance>,
    guarantees: Vec<Guarantee>,
}
```

---

## State Structure

<img width="600px" src="../../assets/img/7-Polkadot/jam-state.png" />

```rust
struct State {
    authorizer_pool: Vec<Vec<Hash>>,         // α
    recent_history: RecentHistory,           // β
    safrole: Safrole,                        // γ
    services: HashMap<u64, ServiceAccount>,  // δ
    entropy_pool: EntropyPool,               // η
    ...
}
```
---


## State Transition Function

<img width="600px" src="../../assets/img/7-Polkadot/jam-stf.png" />


```rust
let new_state = state_transition(state, block) 

fn state_transition(state: &State, block: Block) -> State {
  // Logic to update state with new block
}
```

---

## State Dependencies
<img width="600px" src="../../assets/img/7-Polkadot/jam-stf-deps.png" />


```rust
let timeslot_ = get_timeslot(h);
let history_daga = get_history_data(h, &state.recent_history);
let history_ = get_history_(h, &ext.tickets, &history_daga, c);
```

---

## Data Encoding

<img width="600px" src="../../assets/img/7-Polkadot/jam-encoding1.png" />


![Screenshot 2024-11-09 at 11.41.12](https://hackmd.io/_uploads/ryKe_P2WJe.png =80%x)
![Screenshot 2024-11-09 at 11.59.42](https://hackmd.io/_uploads/BkhHhv3bJl.png =80%x)

```Elixir!
  def e(nil), do: <<>>    
  
  def e(x) when is_binary(x), do: x
  
  def e(%VariableSize{} = x), do: e(x.size) <> e(x.value)
```

---

## Block Encoding

![Screenshot 2024-11-09 at 11.48.50](https://hackmd.io/_uploads/ryWptw3WJg.png)

---

## Block Encoding

![Screenshot 2024-11-09 at 11.48.50](https://hackmd.io/_uploads/ryWptw3WJg.png)

```Elixir
  def e(%Block{extrinsic: e, header: h}), do: e({h, e})

  def e(%Block.Extrinsic{} = ex), 
    do: e({vs(ex.tickets), ex.disputes, vs(ex.preimages), 
     vs(ex.assurances), vs(ex.guarantees)
    })
```

---

## PVM
![Screenshot 2024-11-10 at 14.06.23](https://hackmd.io/_uploads/HJJKjRa-1g.png)

```Elixir
  @spec f(
    n_integer(), n_integer(), list(n_integer()), Memory.t()
    ) :: {n_integer(), list(integer()), Memory.t()}
  def f(n, gas, registers, memory) do
    if n == @gas do
      Host.remaining_gas(gas, registers, memory)
    else
      {gas - 10, 
       Enum.take(registers, 7) ++ 
       [@what | Enum.drop(registers, 8)], 
       memory}
    end
  end
```

---

## State Merklization

![Screenshot 2024-10-21 at 18.01.12](https://hackmd.io/_uploads/rJGNK-ElJx.png =80%x)

```Elixir!
def merkelize_state(t) do
  merkelize(
   for {k, v} <- t, do: {bits(k), {k, v}} |> Enum.into(%{})
  )
end
```

---

## Conclusion

- Start coding to understand JAM from a developer's perspective
- Elixir functional features reduces learning curve
- Faster development
- Functional alignment with math
- Reduced complexity

---

## Jamixir

![Screenshot 2024-11-09 at 19.43.26](https://hackmd.io/_uploads/Sk0gtAh-Je.png =150x)


Join us
![Screenshot 2024-11-10 at 15.11.48](https://hackmd.io/_uploads/S1G05JAb1x.png =300x)



