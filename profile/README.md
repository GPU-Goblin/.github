# GPU Goblin

GPU Goblin is a computing grid for scientific research. People lend the graphics card or processor
of their computer; researchers use these machines together to train models and run large
computations that their own hardware cannot handle.

[gpugoblin.com](https://gpugoblin.com) · [Download](https://gpugoblin.com/download/) ·
[Project status](https://github.com/GPU-Goblin/gg-server/blob/main/docs/STATUS.md) ·
contact@gpugoblin.com

## How it works

1. A researcher describes the computation in Python with the `gpugoblin` package: an ordinary
   PyTorch model is captured with `torch.export` and translated into a model description. No
   Python code is sent; what leaves the researcher's machine is that description and the input
   tensors.
2. The server, at grid.gpugoblin.com, splits the work into tasks and assigns them to contributors'
   machines, within the limits each owner sets: when to lend, how much memory, which card.
3. On each machine, GPU Goblin's own executor computes the task in a sandbox that cannot reach the
   network or the owner's files: bubblewrap, Landlock and seccomp on Linux; an AppContainer inside
   a Job Object on Windows.
4. A validator recomputes each result before it is accepted. An accepted task produces a signed
   receipt and one entry in the credit ledger. Credits count contributions; they are not money.

## Status (October 2026)

- Version 0.1.1 of the contributor software is published and signed (release key fingerprint
  `SHA256:673XukOsx9kY85im+4qIA2IRxZU3+bEFVaD2VZwyBcM`). On Linux it computes on the processor, on
  graphics cards through Vulkan, and on NVIDIA cards through CUDA.
- On Windows, the processor engine works and has been tested on a virtual machine. Graphics cards
  on Windows are being tested on real hardware and are not offered yet.
- The grid is in beta. Anyone can create an account and lend a machine; researchers request access
  from their account page.
- [STATUS.md](https://github.com/GPU-Goblin/gg-server/blob/main/docs/STATUS.md) lists what works,
  how it was measured, and what is not done yet. It is updated with the code.

## Repositories

| Repository | Contents |
|---|---|
| [gg-server](https://github.com/GPU-Goblin/gg-server) | The server (scheduling, verification, credits), the validator, the `gg` command line, the documentation and the release tooling. The place to start. |
| [gg-worker](https://github.com/GPU-Goblin/gg-worker) | The contributor software: worker, sandboxed executor, desktop application and installers, for Linux and Windows. |
| [gg-python](https://github.com/GPU-Goblin/gg-python) | `gpugoblin`, the Python package and PyTorch driver for researchers. |
| [gg-core](https://github.com/GPU-Goblin/gg-core) | Shared libraries: domain model, signed protocol, approved computations, client of the server. |
| [gg-web](https://github.com/GPU-Goblin/gg-web) | The sources of gpugoblin.com, in fifteen languages. |
| [gg-console](https://github.com/GPU-Goblin/gg-console) | The operations console. Planned; no code yet. |

## Licence

[PolyForm Noncommercial 1.0.0](https://polyformproject.org/licenses/noncommercial/1.0.0/): free
for research and any non-commercial use, source available, not open source in the OSI sense.
Commercial use requires the author's agreement.

## Author and contact

Designed and developed by Nicolas Michel, member of [LAAS-CNRS](https://www.laas.fr) in Toulouse.
GPU Goblin is a personal project, not an official service of CNRS or LAAS-CNRS.
Write to contact@gpugoblin.com; report security issues privately through the "Report a
vulnerability" button of the repository concerned.
