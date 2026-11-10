docker inspect
docker cp
docker stats

docker run --rm \
  -v my_volume:/data:ro \
  -v "$(pwd)":/backup \
  alpine \
  tar czf /backup/my_volume.tar.gz -C /data .