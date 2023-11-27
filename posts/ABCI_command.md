rsync -rv --exclude '**.pt' --exclude 'data/*' --exclude 'dust_box/*' --exclude 'wandb/*' ./source/ abci:/distination

qrsh -g g_id -l resource=1

qsub -g g_id run_job.sh

qstat

show_point

qdel -n task_name
