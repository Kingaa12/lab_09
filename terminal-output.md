```sh
node generate-token.js '{"movie" : "Dune 2.", "snack-money": "$9"}' secret-message > token
```
*I deleted everything before the base64 stringfrom the token file* 

```sh
node decode-token.js $(cat token)
```
```
Header: { alg: 'HS256', typ: 'JWT' }
Payload: {
  movie: 'Dune 2.',
  'snack-money': '$9',
  iat: 1712785902,
  exp: 1712789502
}
```
```sh
node verify-token.js $(cat token) secret-message
```
```
Token is valid. Payload: {
  movie: 'Dune 2.',
  'snack-money': '$9',
  iat: 1712785902,
  exp: 1712789502
}
```

### making sure the fake token can be decoded
```sh
node decode-token.js $(cat faketoken)
```
```
Header: { alg: 'HS256', typ: 'JWT' }
Payload: {
  movie: 'Dune 2.',
  'snack-money': '$9999',
  iat: 1712787350,
  exp: 1712790950
}
```
### Attempt to verify the fake token 
```sh
node verify-token.js $(cat faketoken) secret-message
```
```
Invalid token: invalid signature
```