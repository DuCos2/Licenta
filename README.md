# NetHack Agent

Agent de reinforcement learning pentru NetHack, antrenat cu [Sample Factory](https://github.com/alex-petrenko/sample-factory) (APPO) pe mediul `nethack_challenge` din [NLE](https://github.com/heiner/nle).

## Structura

- `sample-factory/` – submodule git cu Sample Factory (repo-ul oficial)
- `patches/sample-factory.patch` – modificările mele în Sample Factory (`core.py`, `tile_tty.py`)
- `train_dir/` – configul și logurile antrenamentului meu
- `requirements.txt` – pachetele Python folosite

Checkpoint-urile modelelor (`*.pth`, ~71 MB fiecare) nu sunt în repo.

## Instalare (macOS)

```bash
git clone --recurse-submodules <URL-ul acestui repo>
cd nethack_agent
python3.11 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
cd sample-factory
git apply ../patches/sample-factory.patch
pip install -e .
```

## Rulare model

Din folderul `sample-factory`, cu venv-ul activat:

```bash
python -m sf_examples.nethack.enjoy_nethack --env=nethack_challenge --train_dir=./train_dir --experiment=sample_factory_human_monk --device=cpu --no_render --max_num_episodes=10
```

- `--device=cpu` e obligatoriu pe Mac (nu există CUDA).
- Fără `--no_render` vezi jocul în terminal.
- Pentru modelul meu: `--train_dir=../train_dir` (are nevoie de checkpoint-urile `.pth` în `train_dir/sample_factory_human_monk/checkpoint_p0/`).
