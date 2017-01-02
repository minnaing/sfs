REMOTE_HOST = "username@domain"
REMOTE_PATH = "/var/www"
LOCAL_PATH  = `PWD`

push:
	rsync -vrltgoD $(LOCAL_PATH) $(REMOTE_HOST):$(REMOTE_PATH)

pull:
	rsync -vrltgoD $(REMOTE_HOST):$(REMOTE_PATH) $(LOCAL_PATH)

ssh:
	ssh -t $(REMOTE_HOST) "cd $(REMOTE_PATH); /bin/bash"

info:
	@echo " --- [ " $(REMOTE_HOST) " ] --- "
	@echo " Remote Path : " $(REMOTE_PATH)
	@echo " Local Path  : " $(LOCAL_PATH)
