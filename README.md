## 開発環境準備
conda-env list
conda create -n ops-lambda-ami-backup python=3.7

activate ops-lambda-ami-backup

## pip update
python -m pip install --upgrade pip
pip freeze | Out-File -Encoding UTF8 .\requirements.txt

## package install
pip install --requirement ./requirements.txt
pip install --requirement ./requirements.txt --target ./src/vendor/

## test
sam validate -t ./deploy/templates/template.yml
sam local invoke AMIBackupFunction --region ap-northeast-1 --template ./deploy/templates/template.yml --event ./tests/event_file.json
