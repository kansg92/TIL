



docker compose ps



docker compose down -v



docker compose down

docker compose up -d

docker compose up -d --build ## build까지

docker compose down && docker compose build --no-cache && docker compose up -d ## 확실한 리빌드.. 캐시까지 지우기

 docker compose logs -f wiki-bot ## log확인..



docker compose up -d --force-recreate





docker bash 실행

docker compose exec <server : 서비스이름임. name말고> bash





docker compose run --rm sync ## 서비스 바로실행..(1회성 실행 + **끝나면 컨테이너 삭제**)

