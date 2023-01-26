start:
	@echo "Starting container"
	@docker compose -f docker-compose.yml up

start-bg:
	@echo "Starting container"
	@docker compose -f docker-compose.yml up -d

restart:
	@echo "Restarting container"
	@docker compose -f docker-compose.yml down
	@docker compose -f docker-compose.yml up -d

stop:
	@echo "Stopping container"
	@docker compose -f docker-compose.yml down

shell:
	@echo "Shelling into container"
	@docker exec -it postgres_db_logical_slave bash