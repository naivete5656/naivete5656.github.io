# ABCIでよく使うcommand一覧

## data transfer
```/bin/bash
rsync -rv --exclude '**.pt' --exclude 'data/*' ./source/ abci:/distination
```
## job 系
Interactive run
```
qrsh -g g_id -l resource=1
```

Batch run
```
qsub -g g_id run_job.sh
```

Job の状況確認
```
qstat
```

Job の削除
```
qdel -n task_name
```

ポイントの確認
```
show_point
```

### 環境作成系

```
source /etc/profile.d/modules.sh
module load cuda/11.8 cudnn/8.7 python/3.10
python3 -m venv ~/venv/cond_llm
source ~/venv/cond_llm/bin/activate
```

### Example of scripts
```
#!/bin/bash

#$ -l rt_G.small=1
#$ -l h_rt=24:00:00
#$ -N mask
#$ -o mask.log
#$ -j y
#$ -cwd

set -e

source /etc/profile.d/modules.sh
module load cuda/11.8 cudnn/8.7 python/3.10
source ~/venv/cond_llm/bin/activate

accelerate launch --mixed_precision=fp16 --num_machines=1 --num_processes=1 ./scripts/train.py --in_ch 64 --data_path transrate_data/$2/feats_v2 --internal_dim 128 --fold $1 --training_step 200000\
        --savesteps 10000 --diffusion GaussianDiffusion  --model unet --save_path output/$2 --mask_type randn --ckpt_dir ckpt/diffusion/$2 --run_name new_dataset_unet_mask --latest_only

# accelerate launch --mixed_precision=fp16 --num_machines=1 --num_processes=1 ./scripts/train.py --in_ch 64 --data_path transrate_data/her2/feats_v2 --internal_dim 256 --fold 4 --training_step 10\
#         --batch_size 16 --savesteps 5 --diffusion GaussianDiffusion  --mask_type randn --ckpt_dir ckpt/diffusionv2/her2 --run_name mask --latest_only
# module load cuda/12.2/12.2.0 cudnn/8.9/8.9.5 python/3.10/3.10.10
```

