*Wednesday, January 21st, 2026* by **devP**+

# Vi / Vim Commands

## Comment Multiple Lines at Once

1. Get into Visual Mode
`Ctrl + V`

2. Select the lines using up and down arrows keys or J and K Keys
3. Enter `:` Key
4. It automatically prepend the range `'<,'>`
5. Enter **Normal Command** it by adding `norm` as such: `'<,'>norm`
6. End it by adding `I#` for commenting with `#` or the commenting character required (ie: `/`)
7. Hit Enter key
8. Final Result:  `:'<,'>norm I#`