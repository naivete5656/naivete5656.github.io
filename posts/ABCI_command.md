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
