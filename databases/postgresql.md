# PostgreSQL Notes

## Getting Started

For any new postgresql install, you can start here with a new user.

* Default postgresql user: `postgresql`

* Log in first 
`psql -u postgresql`

* Create new user
`CREATE USER <user>;`

* Create Role for user with new password
`CREATE ROLE <user> WITH PASSWORD 'very_secure_password';`

* Add role to user
ie: Add LOGIN role to user 
`ALTER ROLE <user> LOGIN;`