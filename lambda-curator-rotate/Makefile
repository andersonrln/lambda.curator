all: package
.PHONY : all virtualenv package awspush awsupdate

FUNCTION_NAME?=lambda-curator-rotate
IAM_ROLE?=arn:aws:iam::827461279864:role/es-cleanup-lambda
AWS_REGION?=sa-east-1

virtualenv: requirements.txt
	virtualenv .venv
	set -e ; . .venv/bin/activate ; pip install --upgrade pip ; pip install --upgrade setuptools ; pip install -r requirements.txt

package: bootstrap.py requirements.txt *.yml
	$(eval TEMPDIR:=$(shell mktemp -d))
	pip install -r requirements.txt -t $(TEMPDIR)
	cp $^ $(TEMPDIR)
	cd $(TEMPDIR) ; zip -r $(FUNCTION_NAME).zip *
	mv $(TEMPDIR)/$(FUNCTION_NAME).zip .

awspush: lambda-curator-rotate.zip
	aws lambda create-function \
	--region $(AWS_REGION) \
	--function-name $(FUNCTION_NAME) \
	--zip-file fileb://$< \
	--role $(IAM_ROLE) \
	--handler bootstrap.lambda_handler \
	--runtime python2.7

awsupdate: lambda-curator-rotate.zip
	aws lambda update-function-code \
	--region $(AWS_REGION) \
	--function-name $(FUNCTION_NAME) \
	--zip-file fileb://$< \