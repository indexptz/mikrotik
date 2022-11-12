:global maclist
:local reglist
:local token "https://script.google.com/macros/s/XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX/exec\?mac="
:foreach i in=[/interface wireless registration-table find] do={
	:local regmac [/interface wireless registration-table get $i value-name=mac-address]
	:local cnt 0
	:set $reglist ($reglist, $regmac);
	:foreach i in=$maclist do={
		:if ($i = $regmac) do={
			:set $cnt ($cnt+1);
		}
	}
	:if ($cnt = 0) do={
		:set $maclist ($maclist, $regmac);
		:tool fetch url=($token.$regmac."&state=in&mode=location") output=none;
	}
}
:foreach i in=$maclist do={
	:if ([/len [find key=$i in=$reglist]]>0) do={
	} else={
		:set $maclist $reglist;
		:tool fetch url=($token.$i."&state=out&mode=location") output=none;
	}
}
