<div align="center">

## Connect 4


</div>

### Description

This code will enable you to, in ASP, play a game of connect 4 with 2 people sitting at the same PC.
 
### More Info
 
Just a click

Calculates when a winning line has been entered.


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Steve Fitzpatrick](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/steve-fitzpatrick.md)
**Level**          |Intermediate
**User Rating**    |3.7 (11 globes from 3 users)
**Compatibility**  |ASP \(Active Server Pages\)
**Category**       |[Games](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/games__4-13.md)
**World**          |[ASP / VbScript](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/asp-vbscript.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/steve-fitzpatrick-connect-4__4-6141/archive/master.zip)

### API Declarations

This is visitware, you are permitted to use the ware, as long as you wisit the author's other site at http://www.cxcx.cx


### Source Code

```
PLAY.ASP'''''''''''''''''''''''''''''''''''''''
<%
'Initialise variables
dim NewMatrix(12,14)
'Initialise matrix for start of game
for counterrow = 1 to 12
	for countercol = 1 to 14
		NewMatrix(counterrow, countercol) = 0
	next
next
session("matrix") = NewMatrix
session("player") = 1
response.redirect "connect4.asp"
%>
''''''''''''''''''''''''''''''''''''''''''''''''''
CONNECT4.ASP''''''''''''''''''''''''''''''''''''''
''Connect 4 in ASP written by Steve Fitzpatrick April 2000
''
''Program is for 2 players sitting at the same pc
''
''This program is freeware and may be freely distributed so
''long as this banner remains at the top of the source code
''
''Contact Steve Fitzpatrick at steve@cxcx.cx
''Website is http://www.cxcx.cx
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''
%>
<%
dim player
dim counterrow
dim countercol
dim row
dim col
dim theimage
dim matrix
dim onebelow
dim flagged
player = session("player")
matrix = session("matrix")
%>
<%
flagged = 0
row = request.querystring("row")
col = request.querystring("col")
if player mod 2 = 1 then
 	matrix(row,col) = 1
else
	matrix(row,col) = 10
end if
%>
<BR>
   &nbsp;
<table align="center" border="0" cellpadding="0" cellspacing="0" height="180">
<%for row = 4 to 9%>
	<tr>
	<%
	for col = 4 to 10
	if matrix(row,col) = 1 then theimage="images/c4blue.gif"
	if matrix(row,col) = 10 then theimage="images/c4red.gif"
	if matrix(row,col) = 0 then theimage="images/c4non.gif"
		if row = 9 then
			onebelow = true
		else
			if matrix(row+1,col) = 0 then
				onebelow = false
			else
				onebelow = true
			end if
		end if
		if matrix(row,col) = 0 and onebelow=True then %>
		<td width="30" style="border-style: solid; border-width: 1" height="30"><a href="connect4.asp?row=<%=row%>&col=<%=col%>"><img align="center" border="0" src="<%=theimage%>"></a></td>
		<% else %>
		<td width="30" style="border-style: solid; border-width: 1" height="30"><img align="center" border="0" src="<%=theimage%>"></td>
		<% end if %>
		<%
	next
	%>
	</tr>
<%
next
%>
</table>
<%
'Code to check if 4 have been placed in a row, can only happen after the 7th go at teh earliest.
if player>= 7 then
	'declare target sum of 4 adjascent squares (4 for player one, 40 for player two)
	dim target
	if player mod 2 = 1 then target = 4
	if player mod 2 = 0 then target = 40
	dim total1, total2, total3, total4
	'declare constant for check algorithm
	dim k
	row = request.querystring("row")
	col = request.querystring("col")
	'Check for 4 in a row - Killer Bob style
	for k = 0 to 3
		total1 = matrix(row-k,col) + matrix(row-k+1,col) + matrix(row-k+2,col) + matrix(row-k+3,col)
		total2 = matrix(row,col-k) + matrix(row,col-k+1) + matrix(row,col-k+2) + matrix(row,col-k+3)
		total3 = matrix(row-k,col-k) + matrix(row-k+1,col-k+1) + matrix(row-k+2,col-k+2) + matrix(row-k+3,col-k+3)
		total4 = matrix(row+k,col-k) + matrix(row+k-1,col-k+1) + matrix(row+k-2,col-k+2) + matrix(row+k-3,col-k+3)
		if ((total1=4) or (total2=4) or (total3=4) or (total4=4) or (total1=40) or (total2=40) or (total3=40) or (total4=40)) and flagged=0 then
			response.write "player " & (player mod 2) +1 & " wins!"
			flagged = 2
		%>
		<BR><P><a href="play.asp">Click here for a new game</a>
		<%
		end if
	next
end if
%>
<%
if (player=43 and flagged=0) then
		flagged = 2
%>
<BR><P>It's a draw!!<p><a href="play.asp">Click here for a new game</a>
<%
	end if
player = player + 1
session("row") = row
session("col") = col
session("matrix") = matrix
session("player") = player
%>
```

