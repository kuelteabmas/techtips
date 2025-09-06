# Pi-Hole Notes

*Thursday, February 20th, 2025* by **devP**

## Watch YouTube video not being saved in YouTube History

* Whitelist the domain **`s.youtube.com`**

### Steps
1. If you're running Pi-Hole via Docker, log in to the container `docker exec -t <container_id> bash` 
2. run `pihole -w s.youtube.com`

---