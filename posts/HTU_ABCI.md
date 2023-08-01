## Public keyの登録

詳しくは以下の資料参照
https://abci.ai/ja/how_to_use/data/ABCI_handson_2020.pdf

sshのコマンド
'''
ssh -L 10022:es:22 -l acc12552uq as.abci.ai -i .ssh/abciid_rsa

ssh -L 10022:es:22 -l abci_uid as.abci.ai -i secret_key_path
'''
