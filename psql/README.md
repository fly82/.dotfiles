Append code below to .bashrc or .bash_profile

```
export YELLOW=`echo -e '\033[1;33m'`
export RED=`echo -e '\033[1;31m'`
export LIGHT_CYAN=`echo -e '\033[1;36m'`
export GREEN=`echo -e '\033[1;32m'`
export GREY=`echo -e '\033[1;37m'`
export NOCOLOR=`echo -e '\033[0m'`

PSQL_PAGER="sed \"s/\([[:space:]]\+[0-9.\-]\+\)$/${LIGHT_CYAN}\1$NOCOLOR/;"
PSQL_PAGER+="s/\([[:space:]]\+[0-9.\-]\+[[:space:]]\)/${LIGHT_CYAN}\1$NOCOLOR/g;"
PSQL_PAGER+="s/\([[:space:]]\-[0-9.\-]\+[[:space:]]\)/${RED}\1$NOCOLOR/g;"
PSQL_PAGER+="s/∅/${GREEN}∅$NOCOLOR/g;s/|/$YELLOW|$NOCOLOR/g;s/^\([-+]\+\)/$YELLOW\1$NOCOLOR/\" 2>/dev/null | less"
```
Append code below to .bash_aliases
```
alias psql='PAGER=${PSQL_PAGER} LESS="-iMSx4 -FXR" psql -h localhost -U postgres'
```
or
```
alias psql='PGPASSFILE=.pgpass PAGER=${PSQL_PAGER} LESS="-iMSx4 -FXR" psql -h $(cut -d: -f1 ${PGPASSFILE}) -U postgres'
```
