---
title: Add Line
description: Demonstrates how to construct a line from two points.
author: steve@mcneel.com
apis: ['RhinoCommon']
languages: ['C#', 'Python', 'VB']
platforms: ['Windows', 'Mac']
categories: ['Adding Objects']
origin: http://wiki.mcneel.com/developer/rhinocommonsamples/addline
order: 1
keywords: ['add', 'line']
layout: code-sample-rhinocommon
---

```cs
partial class Examples
{
  public static Rhino.Commands.Result AddLine(Rhino.RhinoDoc doc)
  {
    Rhino.Input.Custom.GetPoint gp = new Rhino.Input.Custom.GetPoint();
    gp.SetCommandPrompt("Start of line");
    gp.Get();
    if (gp.CommandResult() != Rhino.Commands.Result.Success)
      return gp.CommandResult();

    Rhino.Geometry.Point3d pt_start = gp.Point();

    gp.SetCommandPrompt("End of line");
    gp.SetBasePoint(pt_start, false);
    gp.DrawLineFromPoint(pt_start, true);
    gp.Get();
    if (gp.CommandResult() != Rhino.Commands.Result.Success)
      return gp.CommandResult();

    Rhino.Geometry.Point3d pt_end = gp.Point();
    Rhino.Geometry.Vector3d v = pt_end - pt_start;
    if (v.IsTiny(Rhino.RhinoMath.ZeroTolerance))
      return Rhino.Commands.Result.Nothing;

    if (doc.Objects.AddLine(pt_start, pt_end) != Guid.Empty)
    {
      doc.Views.Redraw();
      return Rhino.Commands.Result.Success;
    }
    return Rhino.Commands.Result.Failure;
  }
}
```
{: #cs .tab-pane .fade .in .active}


```vbnet
Partial Friend Class Examples
  Public Shared Function AddLine(ByVal doc As Rhino.RhinoDoc) As Rhino.Commands.Result
	Dim gp As New Rhino.Input.Custom.GetPoint()
	gp.SetCommandPrompt("Start of line")
	gp.Get()
	If gp.CommandResult() <> Rhino.Commands.Result.Success Then
	  Return gp.CommandResult()
	End If

	Dim pt_start As Rhino.Geometry.Point3d = gp.Point()

	gp.SetCommandPrompt("End of line")
	gp.SetBasePoint(pt_start, False)
	gp.DrawLineFromPoint(pt_start, True)
	gp.Get()
	If gp.CommandResult() <> Rhino.Commands.Result.Success Then
	  Return gp.CommandResult()
	End If

	Dim pt_end As Rhino.Geometry.Point3d = gp.Point()
	Dim v As Rhino.Geometry.Vector3d = pt_end - pt_start
	If v.IsTiny(Rhino.RhinoMath.ZeroTolerance) Then
	  Return Rhino.Commands.Result.Nothing
	End If

	If doc.Objects.AddLine(pt_start, pt_end) <> Guid.Empty Then
	  doc.Views.Redraw()
	  Return Rhino.Commands.Result.Success
	End If
	Return Rhino.Commands.Result.Failure
  End Function
End Class
```
{: #vb .tab-pane .fade .in}


```python
import Rhino
import scriptcontext
import System.Guid

def AddLine():
    gp = Rhino.Input.Custom.GetPoint()
    gp.SetCommandPrompt("Start of line")
    gp.Get()
    if gp.CommandResult()!=Rhino.Commands.Result.Success:
        return gp.CommandResult()
    pt_start = gp.Point()

    gp.SetCommandPrompt("End of line")
    gp.SetBasePoint(pt_start, False)
    gp.DrawLineFromPoint(pt_start, True)
    gp.Get()
    if gp.CommandResult() != Rhino.Commands.Result.Success:
        return gp.CommandResult()
    pt_end = gp.Point()
    v = pt_end - pt_start
    if v.IsTiny(Rhino.RhinoMath.ZeroTolerance):
        return Rhino.Commands.Result.Nothing

    id = scriptcontext.doc.Objects.AddLine(pt_start, pt_end)
    if id!=System.Guid.Empty:
        scriptcontext.doc.Views.Redraw()
        return Rhino.Commands.Result.Success
    return Rhino.Commands.Result.Failure

if __name__=="__main__":
    AddLine()
```
{: #py .tab-pane .fade .in}
