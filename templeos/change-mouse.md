# TempleOS Help

## Change Mouse Cursor
Edit `C:/Adam/Gr/GrComposites.HC.Z`, line `0298`
You can't use custom sprites with `Sprite3(dc,x,y,0,<*>);` since it's not declared yet.
Manually draw the cursor with Gr\*() subfunctions
You can also create a custom script with a redefinition of DrawStdMs() and reassignment to `gr.fp_draw_ms`:
```HolyC
public U0 DrawNewStdMouse(CDC *dc, I64 x, I64 y)
{
	<1> // Your sprite or sprite pointer
	// $SP,"<1>", BI=1,BP="C:/Home/cursor,1"$$ER$
	Sprite3(dc, x,y,0, <1>);
	// Sprite3(dc, x,y,0, $IB,"<1>",BI=1$);
}
gr.ph_draw_ms=&DrawNewStdMouse;
```
