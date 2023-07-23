# EMLOv3 | Assignment 7

[![pytorch](https://img.shields.io/badge/PyTorch_1.13+-ee4c2c?logo=pytorch&logoColor=white)](https://pytorch.org/get-started/locally/)
[![lightning](https://img.shields.io/badge/-Lightning_2.0+-792ee5?logo=pytorchlightning&logoColor=white)](https://pytorchlightning.ai/)
[![hydra](https://img.shields.io/badge/Config-Hydra_1.3+-89b8cd)](https://hydra.cc/)
[![black](https://img.shields.io/badge/Code%20Style-Black-black.svg?labelColor=gray)](https://black.readthedocs.io/en/stable/)


## Hyperparameter Optimization using <b>Optuna</b>
The module is called <em>'gold'</em>.
This module supports optimiztion for following parameters (for GPT model):

    block_size
    n_embed
    n_heads
    drop_p
    n_decoder_blocks : This is the number of GPTDecoderBlock used in self.blocks of GPT

The search space is defined in the yaml file in hparams_search in configs. The data used is Harry patter books consolidated.


## To run

1. Git clone this repo

```
git clone https://github.com/jha-vikas/EMLO_session07-HParam-Optimization
```

2. Move inside the repor fodler
```
cd EMLO_session07-HParam-Optimization
```

3. Install requirements & gold moduel
```
pip install -r requirements.txt && pip install -e .
```

4. Use tuner to get best LR & batch size.
   Run LR_and_Batch_size_finder.ipynb from notebooks folder with required changes.

5. Train (Adjust parameters of batch_size, num_workers & LR)
```
gold_train data.batch_size=1024 data.num_workers=2 model.learning_rate=0.001
```


### Best hyperparameters & loss(val) value:
```
block_size: 8
n_embed: 256
n_heads: 4
drop_p: 0.08
n_decoder_blocks: 4

Best val/loss value: 2.864
```

- In inital runs, n_heads of 8, 16 & 32 were also considered. However, with 32 as head & 256 as embedding size, with A6000 as GPU, it took 2+ hrs for one iteration. Hence, it was stopped and a smaller number of iteration and reduced values of heads were considered.
- Inital startup trials considered: 5
- Total trials: 10
- Time taken: ~4.5 hrs
- Result comparison between runs:

### Intial run (partial as it was consuming too much resources)
![Intial run comparison](screenshots/Inital_run_comparison.jpg)

### Final run (All 10 runs completed)
![Final run comparison](screenshots/session07_compare.jpg)


## Author

- Vikas Jha
