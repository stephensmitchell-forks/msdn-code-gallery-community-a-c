# Calculator Application / Phone Application & Microchip code Visual Studio 2015
## Requires
- Visual Studio 2015
## License
- MS-LPL
## Technologies
- usb
- Windows XP
- Phone Application
- Windows 8.1 Professional
- Embedded Hardware
## Topics
- Windows
- Visual Basic.NET
- usb
- Phone Application
- Integration with USB and Embedded Hardware
## Updated
- 04/02/2017
## Description

<h1>Introduction</h1>
<p><em>The Calculator Application or Phone Application is upgraded to Visual Studio 2015. The program is similar to the previous versions without the Webcam. The upgrade provides the use with the latest sample of the Phone Application/ Calculator Application.</em></p>
<p><em>The Phone Application is an example of software and hardware intergration utilizing Microsoft Visual Studio and Microchip devices. The existing hardware is obtainanble through Engineering and Computer Works(<a href="http://engineeeringcomputerworks.com">http://engineeeringcomputerworks.com</a>).
</em></p>
<p><em>The software is able to control games and is able to utilize the hardware as a controller. There are multiple applications of the software and hardware and could be utilised as control systems and stand alone systems.</em></p>
<p><em>For further information on the hardware and software, please contact as below Engineering and Computer Works. (<a href="http://engineeeringcomputerworks.com">http://engineeeringcomputerworks.com</a>)<br>
</em></p>
<h1><span>Building the Sample</span></h1>
<p><em>Visual Studio 2015 is required.</em></p>
<p><span style="font-size:20px; font-weight:bold">Description</span></p>
<p><em>The software is upgraded to Visual Studio Version 2015.</em><em>&nbsp;</em></p>
<p><em>The Phone Application is an example of software and hardware intergration utilizing Microsoft Visual Studio 2015 and Microship devices from Engineering and Computer Works.(<a href="http://engineeeringcomputerworks.com">http://engineeeringcomputerworks.com</a>).
<br>
</em></p>
<p>&nbsp;</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>Visual Basic</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">vb</span>
<pre class="hidden">'http://msdn.microsoft.com/en-us/library/ms171728(VS.80).aspx
'
'&quot;Visual Basic Developer Center&quot;
'http://msdn.microsoft.com/en-us/vbasic/default.aspx?pull=/library/en-us/vbcon/html/vboriintroductiontovisualbasic70forvisualbasicveterans.asp
Imports System
Imports System.IO
Imports System.IO.Ports
Imports System.Timers

'Public Class Timer1

Public Class Form1

    'Private Property b As String

    'Private Property OpenMode() As String

    'Create a delegate function for this thread that will take
    '  in a string and will write it to the txtDataReceived textbox
    Delegate Sub SetTextCallback(ByVal [text] As String)

    '****************************************************************************
    '   Function:
    '       private void UpdateCOMPortList()
    '
    '   Summary:
    '       This function updates the COM ports listbox.
    '
    '   Description:
    '       This function updates the COM ports listbox.  This function is launched 
    '       periodically based on its Interval attribute (set in the form editor under
    '       the properties window).
    '
    '   Precondition:
    '       None
    '
    '   Parameters:
    '       None
    '
    '   Return Values
    '       None
    '
    '   Remarks:
    '       None
    '***************************************************************************
    Private Sub UpdateCOMPortList()
        Dim s As String
        Dim i As Integer
        Dim foundDifference As Boolean

        i = 0
        foundDifference = False
        'If the number of COM ports is different than the last time we
        '  checked, then we know that the COM ports have changed and we
        '  don't need to verify each entry.

        If lstCOMPorts.Items.Count = SerialPort.GetPortNames().Length Then
            'Search the entire SerialPort object.  Look at COM port name
            '  returned and see if it already exists in the list.
            For Each s In SerialPort.GetPortNames()
                'If any of the names have changed then we need to update 
                '  the list
                If lstCOMPorts.Items(i).Equals(s) = False Then
                    foundDifference = True
                End If
                i = i &#43; 1
            Next s
        Else
            foundDifference = True
        End If

        'If nothing has changed, exit the function.
        If foundDifference = False Then
            Exit Sub
        End If

        'If something has changed, then clear the list
        lstCOMPorts.Items.Clear()

        'Add all of the current COM ports to the list
        For Each s In SerialPort.GetPortNames()
            lstCOMPorts.Items.Add(s)
        Next s
        'Set the listbox to point to the first entry in the list
        lstCOMPorts.SelectedIndex = 0
    End Sub


    '****************************************************************************
    '   Function:
    '       private void timer1_Tick(object sender, EventArgs e)
    '
    '   Summary:
    '       This function updates the COM ports listbox.
    '
    '   Description:
    '       This function updates the COM ports listbox.  This function is launched 
    '       periodically based on its Interval attribute (set in the form editor under
    '       the properties window).
    '
    '   Precondition:
    '       None
    '
    '   Parameters:
    '       object sender     - Sender of the event (this form)
    '       EventArgs e       - The event arguments
    '
    '   Return Values
    '       None
    '
    '   Remarks:
    '       None
    '***************************************************************************/

    Private Sub Timer1_Tick(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Timer1.Tick
        'Update the COM ports list so that we can detect
        '  new COM ports that have been added.
        UpdateCOMPortList()
    End Sub


    '****************************************************************************
    '   Function:
    '       private void btnConnect_Click(object sender, EventArgs e)
    '
    '   Summary:
    '       This function opens the COM port.
    '
    '   Description:
    '       This function opens the COM port.  This function is launched when the 
    '       btnConnect button is clicked.  In addition to opening the COM port, this 
    '       function will also change the Enable attribute of several of the form
    '       objects to disable the user from opening a new COM port.
    '
    '   Precondition:
    '       None
    '
    '   Parameters:
    '       object sender     - Sender of the event (this form)
    '       EventArgs e       - The event arguments
    '
    '   Return Values
    '       None
    '
    '   Remarks:
    '       None
    '***************************************************************************/
    Private Sub btnConnect_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles btnConnect.Click
        'This section of code will try to open the COM port.
        '  Please note that it is important to use a try/catch
        '  statement when opening the COM port.  If a USB virtual
        '  COM port is removed and the PC software tries to open
        '  the COM port before it detects its removal then
        '  an exeception is thrown.  If the execption is not in a
        '  try/catch statement this could result in the application
        '  crashing.
        Try
            'Get the port name from the application list box.
            '  the PortName attribute is a string name of the COM
            '  port (e.g. - &quot;COM1&quot;).
            SerialPort1.PortName = lstCOMPorts.Items(lstCOMPorts.SelectedIndex).ToString()

            'Open the COM port.
            SerialPort1.Open()

            'Change the state of the application objects
            btnConnect.Enabled = False
            lstCOMPorts.Enabled = False
            btnClose.Enabled = True

            'Clear the textbox and print that we are connected.
            txtDataReceived.Clear()
            txtDataReceived.AppendText(&quot;Connected.&quot; &#43; vbCrLf)
            txtDataReceived.Clear()
        Catch ex As Exception
            'If there was an exception, then close the handle to 
            '  the device and assume that the device was removed
            btnClose_Click(Me, e)

        End Try
    End Sub


    '****************************************************************************
    '   Function:
    '       private void btnClose_Click(object sender, EventArgs e)
    '
    '   Summary:
    '       This function closes the COM port.
    '
    '   Description:
    '       This function closes the COM port.  This function is launched when the 
    '       btnClose button is clicked.  This function can also be called directly
    '       from other functions.  In addition to closing the COM port, this 
    '       function will also change the Enable attribute of several of the form
    '       objects to enable the user to open a new COM port.
    '
    '   Precondition:
    '       None
    '
    '   Parameters:
    '       object sender     - Sender of the event (this form)
    '       EventArgs e       - The event arguments
    '
    '   Return Values
    '       None
    '
    '   Remarks:
    '       None
    '***************************************************************************/
    Private Sub btnClose_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles btnClose.Click
        'Reset the state of the application objects
        btnClose.Enabled = False
        btnConnect.Enabled = True
        lstCOMPorts.Enabled = True

        'This section of code will try to close the COM port.
        '  Please note that it is important to use a try/catch
        '  statement when closing the COM port.  If a USB virtual
        '  COM port is removed and the PC software tries to close
        '  the COM port before it detects its removal then
        '  an exeception is thrown.  If the execption is not in a
        '  try/catch statement this could result in the application
        '  crashing.
        Try

            'Dispose the In and Out buffers;
            SerialPort1.DiscardInBuffer()
            SerialPort1.DiscardOutBuffer()
            'Close the COM port
            SerialPort1.Close()
            'If there was an exeception then there isn't much we can
            '  do.  The port is no longer available.
        Catch ex As Exception

        End Try
    End Sub


    '****************************************************************************
    '   Function:
    '       private void serialPort1_DataReceived(  object sender, 
    '                                               SerialDataReceivedEventArgs e)
    '
    '   Summary:
    '       This function prints any data received on the COM port.
    '
    '   Description:
    '       This function is called when the data is received on the COM port.  This
    '       function attempts to write that data to the txtDataReceived textbox.  If
    '       an exception occurs the btnClose_Click() function is called in order to
    '       close the COM port that caused the exception.
    '   
    '   Precondition:
    '       None
    '
    '   Parameters:
    '       object sender     - Sender of the event (this form)
    '       SerialDataReceivedEventArgs e       - The event arguments
    '
    '   Return Values
    '       None
    '
    '   Remarks:
    '       None
    '***************************************************************************/
    Private Sub SerialPort1_DataReceived(ByVal sender As System.Object, ByVal e As System.IO.Ports.SerialDataReceivedEventArgs) Handles SerialPort1.DataReceived
        'The ReadExisting() function will read all of the data that
        '  is currently available in the COM port buffer.  In this 
        '  example we are sending all of the available COM port data
        '  to the SetText() function.
        '
        '  NOTE: the &lt;SerialPort&gt;_DataReceived() function is launched
        '  in a seperate thread from the rest of the application.  A
        '  delegate function is required in order to properly access
        '  any managed objects inside of the other thread.  Since we
        '  will be writing to a textBox (a managed object) the delegate
        '  function is required.  Please see the SetText() function for 
        '  more information about delegate functions and how to use them.
        Try
            SetText(SerialPort1.ReadExisting())
        Catch ex As Exception
            'If there was an exception, then close the handle to 
            '  the device and assume that the device was removed
            btnClose_Click(Me, e)
        End Try

    End Sub


    '****************************************************************************
    '   Function:
    '       private void SetText(string text)
    '
    '   Summary:
    '       This function prints the input text to the txtDataReceived textbox.
    '
    '   Description:
    '       This function prints the input text to the txtDataReceived textbox.  If
    '       the calling thread is the same as the thread that owns the textbox, then
    '       the AppendText() method is called directly.  If a thread other than the
    '       main thread calls this function, then an instance of the delegate function
    '       is created so that the function runs again in the main thread.
    '
    '   Precondition:
    '       None
    '
    '   Parameters:
    '       string text     - Text that needs to be printed to the textbox
    '
    '   Return Values
    '       None
    '
    '   Remarks:
    '       None
    '***************************************************************************/
    Private Sub SetText(ByVal [text] As String)
        'InvokeRequired required compares the thread ID of the
        '  calling thread to the thread ID of the creating thread.
        '  If these threads are different, it returns true.  We can
        '  use this attribute to determine if we can append text
        '  directly to the textbox or if we must launch an a delegate
        '  function instance to write to the textbox.
        If txtDataReceived.InvokeRequired Then
            'InvokeRequired returned TRUE meaning that this function
            '  was called from a thread different than the current
            '  thread.  We must launch a deleage function.

            'Create an instance of the SetTextCallback delegate and
            '  assign the delegate function to be this function.  This
            '  effectively causes this same SetText() function to be
            '  called within the main thread instead of the second
            '  thread.
            Dim d As New SetTextCallback(AddressOf SetText)

            'Invoke the new delegate sending the same text to the
            '  delegate that was passed into this function from the
            '  other thread.
            Invoke(d, New Object() {[text]})
        Else
            'If this function was called from the same thread that 
            '  holds the required objects then just add the text.
            txtDataReceived.Text = (text)
            TextBox5.AppendText(text)
            txtDataReceivedd.AppendText((text))




        End If
    End Sub


    '****************************************************************************
    '   Function:
    '       private void btnSendData_Click(object sender, EventArgs e)
    '
    '   Summary:
    '       This function will attempt to send the contents of txtData over the COM port
    '
    '   Description:
    '       This function is called when the btnSendData button is clicked.  It will 
    '       attempt to send the contents of txtData over the COM port.  If the attempt
    '       is unsuccessful this function will call the btnClose_Click() in order to
    '       close the COM port that just failed.
    '
    '   Precondition:
    '       None
    '
    '   Parameters:
    '       object sender     - Sender of the event (this form)
    '       EventArgs e       - The event arguments
    '
    '   Return Values
    '       None
    '
    '   Remarks:
    '       None
    '***************************************************************************/
    Private Sub btnSendData_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles btnSendData.Click
        'This section of code will try to write to the COM port.
        '  Please note that it is important to use a try/catch
        '  statement when writing to the COM port.  If a USB virtual
        '  COM port is removed and the PC software tries to write
        '  to the COM port before it detects its removal then
        '  an exeception is thrown.  If the execption is not in a
        '  try/catch statement this could result in the application
        '  crashing.
        Try
            'Write the data in the text box to the open serial port
            txtData.Text = &quot;12&quot;
            SerialPort1.Write(txtData.Text)
            ' Button23.PerformClick()
        Catch ex As Exception
            'If there was an exception, then close the handle to 
            '  the device and assume that the device was removed
            btnClose_Click(Me, e)
        End Try
    End Sub

    Private Sub txtDataReceived_MouseClick(ByVal sender As Object, ByVal e As System.Windows.Forms.MouseEventArgs) Handles txtDataReceived.MouseClick
        txtDataReceived.Clear()
    End Sub

    Private Sub txtDataReceived_MouseDoubleClick(ByVal sender As Object, ByVal e As System.Windows.Forms.MouseEventArgs) Handles txtDataReceived.MouseDoubleClick

    End Sub
    Private Sub Test1()
        On Error Resume Next
        'Dim text As String
        Me.TopMost = True
        ' txtDataReceived.Clear()
        Dim i, n
        aTimer = New System.Timers.Timer(10000)
        Me.TopMost = True
        For i = 1 To 10
            Dim msg = &quot;Do you want to continue?&quot;


            ' Display a simple message box.
            MsgBox(msg)

            ' Define a title for the message box. 
            Dim title = &quot;MsgBox Demonstration&quot;

            ' Add the title to the display.
            MsgBox(msg, , i)

            ' Now define a style for the message box. In this example, the 
            ' message box will have Yes and No buttons, the default will be 
            ' the No button, and a Critical Message icon will be present. 
            Dim style = MsgBoxStyle.YesNo Or MsgBoxStyle.DefaultButton2 Or _
                        MsgBoxStyle.Critical

            ' Display the message box and save the response, Yes or No. 
            Dim response = MsgBox(msg, style, title)

            ' Take some action based on the response. 
            If response = MsgBoxResult.Yes &amp; TextBox5.Text = &quot;101&quot; Then
                MsgBox(&quot;YES, continue!!&quot;, , title)
                TextBox3.AppendText(i)
                ' Exit Sub
                '  txtDataReceived.Clear()
            Else
                MsgBox(&quot;NO, stop!!&quot;, , title)
                TextBox3.AppendText(&quot;&quot;)

            End If
            ' Exit Sub
            ' Hook up the Elapsed event for the timer. 
            '   AddHandler aTimer.Elapsed, AddressOf OnTimedEvent

            ' Set the Interval to 2 seconds (2000 milliseconds).


            'For n = 1 To 1
            ' Button24.PerformClick()
            '  TextBox3.Text = i
            '  Timer2.Interval = 2000
            '  Timer2.Enabled = True
            '  Timer2.Start()

            'a:          If Timer2.ToString = &quot;0000&quot; Then
            ' Stop
            ' MsgBox(i)

            ' If Keys.I Then
            'handler:

            '  If MsgBox(i, MsgBoxStyle.YesNo, MsgBoxResult.Yes) Then
            ' If MsgBox(i, MsgBoxResult.Yes) Then



            'Else
            '  ElseIf MsgBoxResult.Yes = 6 Then
            ' TextBox3.AppendText(&quot;&quot;)

            ' End If
        Next i
        'End If
        Exit Sub
    End Sub
    Private Sub txtDataReceived_TextChanged(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles txtDataReceived.TextChanged

        '   Dim a As Integer
        '        a = 2
        For a As Integer = 1 To 2
            '   If txtDataReceived.Text = &quot;1&quot; Or &quot;2&quot; Or &quot;3&quot; Or &quot;4&quot; Or &quot;5&quot; Or &quot;6&quot; Or &quot;7&quot; Or &quot;8&quot; Or &quot;9&quot; Or &quot;0&quot; Then
            'Dim I As Integer
            'For I = 1 To 1000  ' Loop 100 times.
            'Beep()   ' Sound a tone.
            'Next I









            If txtDataReceived.Text = &quot;&#43;&quot; Then
                ' txtDataReceived.AppendText(&quot;0&quot;)
                '  MsgBox(&quot;&#43;&quot;)
                Button23.PerformClick()
                '  ElseIf txtDataReceived.Text = &quot;&#43;&quot; Then 'And txtDataReceived.Text = &quot;&#43;&quot; Then
                Button27.PerformClick()
                txtDataReceived.Clear()
                TextBox5.Clear()
                '  Button24.PerformClick()
                'ElseIf txtDataReceived.Text = &quot;!P&quot; Then
            ElseIf txtDataReceived.Text = &quot;#&quot; Then
                '  txtDataReceived.AppendText(&quot;1&quot;)
                Button26.PerformClick()

                '   btnSendData.PerformClick()
                '  btnSendData.PerformClick()
                ' btnSendData.PerformClick()
                ' btnSendData.PerformClick()
                ' btnSendData.PerformClick()
                ' btnSendData.PerformClick()
                ' btnSendData.PerformClick()
                ' btnSendData.PerformClick()
                Button25.PerformClick()
                txtDataReceived.Clear()
                TextBox5.Clear()
            ElseIf txtDataReceived.Text = &quot;A&quot; Then
                txtDataReceived.Text = &quot;A&quot;
                TextBox5.AppendText(&quot;AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA&quot;)
                '  txtDataReceived.AppendText(&quot;2&quot;)
                'Button11.PerformClick()
            ElseIf txtDataReceived.Text = &quot;b&quot; Then
                txtDataReceived.Text = &quot;B&quot;
                TextBox5.AppendText(&quot;BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB&quot;)
                '  txtDataReceived.AppendText(&quot;2&quot;)
                'Button11.PerformClick()
            ElseIf txtDataReceived.Text = &quot;2&quot; Then
                txtDataReceived.Text = &quot;2&quot; 'Hex(38)
                a = Keys.Up
                TextBox5.AppendText(&quot;2222222222222222222222222222222222222222222222222222222222&quot;)
                ' If txtDataReceived.Text = Hex(38) Then TextBox5.Text = Hex(38)
                '  txtDataReceived.AppendText(&quot;2&quot;)
                'Button11.PerformClick()
            ElseIf txtDataReceived.Text = &quot;8&quot; Then
                txtDataReceived.Text = &quot;8&quot; 'Keys.Down

                TextBox5.AppendText(&quot;888888888888888888888888888888888888888888888888888888888888888&quot;)
                'If TextBox5.Text = &quot;8&quot; Then TextBox5.Text = Keys.Down

            ElseIf txtDataReceived.Text = &quot;4&quot; Then
                txtDataReceived.Text = &quot;4&quot; 'Keys.Left
                TextBox5.AppendText(&quot;4444444444444444444444444444444444444444444444444444444444444444&quot;)
                'If TextBox5.Text = &quot;4&quot; Then TextBox5.Text = Keys.Left
                '  txtDataReceived.AppendText(&quot;2&quot;)
                'Button11.PerformClick()
            ElseIf txtDataReceived.Text = &quot;6&quot; Then
                txtDataReceived.Text = &quot;6&quot; 'Keys.Right
                TextBox5.AppendText(&quot;666666666666666666666666666666666666666666666666666666666666666666666&quot;)
                'If TextBox5.Text = &quot;6&quot; Then TextBox5.Text = Keys.Right
            ElseIf txtDataReceived.Text = &quot;s&quot; Then
                '  txtDataReceived.AppendText(&quot;2&quot;)
                Button11.PerformClick()
            ElseIf txtDataReceived.Text = &quot;t&quot; Then
                '    txtDataReceived.AppendText(&quot;3&quot;)
                Button12.PerformClick()
            ElseIf txtDataReceived.Text = &quot;u&quot; Then
                '   txtDataReceived.AppendText(&quot;4&quot;)
                Button13.PerformClick()
            ElseIf txtDataReceived.Text = &quot;v&quot; Then
                '   txtDataReceived.AppendText(&quot;5&quot;)
                Button14.PerformClick()
            ElseIf txtDataReceived.Text = &quot;w&quot; Then
                '   txtDataReceived.AppendText(&quot;6&quot;)
                Button15.PerformClick()
            ElseIf txtDataReceived.Text = &quot;x&quot; Then
                '   txtDataReceived.AppendText(&quot;7&quot;)
                Button16.PerformClick()
            ElseIf txtDataReceived.Text = &quot;y&quot; Then
                '   txtDataReceived.AppendText(&quot;8&quot;)
                Button17.PerformClick()
            ElseIf txtDataReceived.Text = &quot;p&quot; Then
                '   txtDataReceived.AppendText(&quot;9&quot;)
                Button18.PerformClick()
                '     ElseIf Keys.NumPad6 Then
                '         txtDataReceived.Text = &quot;6&quot;
            ElseIf TextBox5.Text = &quot;P&quot; Then
                TextBox5.Clear()
                '  Else : TextBox5.Clear()
            ElseIf TextBox5.Text = &quot;#&quot; Then
                TextBox5.Clear()
            ElseIf TextBox5.Text = &quot;!&quot; Then
                TextBox5.Clear()
            ElseIf TextBox5.Text = &quot;!#P&quot; Then
                TextBox5.Clear()
            End If
            '  TextBox5.Clear()
        Next

        '            Else
        '           GoTo a
        '            End If
        ' Else
        '  Exit Sub
        '   End If
        ' Me.TopMost = True
        '  Timer2.Stop()


        ' Button24.PerformClick()

    End Sub
    Private Sub test()


        If txtDataReceived.Text = &quot;1&quot; Then
            txtDataReceived.Clear()
            Button10.Select()


            Dim c As Integer
            Dim d As Integer
            Dim ProcID As Integer
            'Dim c As Integer
            'Dim d As Integer
            ProcID = Shell(&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;, AppWinStyle.NormalFocus)
            ' c = &quot;0&quot;
            'My.Forms.Form1.Button10.    
            TextBox2.Text = &quot;0&quot;
            'Me.TopMost = True
            'ProcID = Form1.TextBox2.Text
            Form1a.TextBox1.Text = ProcID
            TextBox1.Text = Form1a.TextBox1.Text
            'MsgBox(ProcID)
            'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
            ProcID = Form1a.TextBox1.Text
            ' ProcID = &quot;Windows Media Player&quot;
            'TextBox1.Text = ProcID
            ' On Error GoTo errorhandler
            c = TextBox1.Text
            'TextBox1.Text = Form1.TextBox1.Text
            TextBox2.Text = Form1a.TextBox3.Text
            AppActivate(&quot;Windows Media Player&quot;)

            My.Computer.Keyboard.SendKeys(&quot;%S&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;%FOn&quot;, True)
            'AppActivate(&quot;Open&quot;)
            My.Computer.Keyboard.SendKeys(&quot;%n&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;1.wma&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;%P&quot;, True)
            'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
            TextBox3.AppendText(&quot;1&quot;)


        ElseIf txtDataReceived.Text = &quot;2&quot; Then
            Button11.Select()
            Dim c As Integer
            Dim d As Integer
            Dim ProcID As Integer
            'Dim c As Integer
            'Dim d As Integer
            ProcID = Shell(&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;, AppWinStyle.NormalFocus)
            ' c = &quot;0&quot;
            'My.Forms.Form1.Button10.    
            TextBox2.Text = &quot;0&quot;
            'Me.TopMost = True
            'ProcID = Form1.TextBox2.Text
            Form1a.TextBox1.Text = ProcID
            TextBox1.Text = Form1a.TextBox1.Text
            'MsgBox(ProcID)
            'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
            ProcID = Form1a.TextBox1.Text
            ' ProcID = &quot;Windows Media Player&quot;
            'TextBox1.Text = ProcID
            ' On Error GoTo errorhandler
            c = TextBox1.Text
            'TextBox1.Text = Form1.TextBox1.Text
            TextBox2.Text = Form1a.TextBox3.Text
            AppActivate(&quot;Windows Media Player&quot;)

            My.Computer.Keyboard.SendKeys(&quot;%S&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;%FOn&quot;, True)
            'AppActivate(&quot;Open&quot;)
            My.Computer.Keyboard.SendKeys(&quot;%n&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;2.wma&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;%P&quot;, True)
            'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
            TextBox3.AppendText(&quot;2&quot;)
            txtDataReceived.Clear()
        ElseIf txtDataReceived.Text = &quot;3&quot; Then
            Button12.Select()
            Dim c As Integer
            Dim d As Integer
            Dim ProcID As Integer
            'Dim c As Integer
            'Dim d As Integer
            ProcID = Shell(&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;, AppWinStyle.NormalFocus)
            ' c = &quot;0&quot;
            'My.Forms.Form1.Button10.    
            TextBox2.Text = &quot;0&quot;
            'Me.TopMost = True
            'ProcID = Form1.TextBox2.Text
            Form1a.TextBox1.Text = ProcID
            TextBox1.Text = Form1a.TextBox1.Text
            'MsgBox(ProcID)
            'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
            ProcID = Form1a.TextBox1.Text
            ' ProcID = &quot;Windows Media Player&quot;
            'TextBox1.Text = ProcID
            ' On Error GoTo errorhandler
            c = TextBox1.Text
            'TextBox1.Text = Form1.TextBox1.Text
            TextBox2.Text = Form1a.TextBox3.Text
            AppActivate(&quot;Windows Media Player&quot;)

            My.Computer.Keyboard.SendKeys(&quot;%S&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;%FOn&quot;, True)
            'AppActivate(&quot;Open&quot;)
            My.Computer.Keyboard.SendKeys(&quot;%n&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;3.wma&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;%P&quot;, True)
            ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
            TextBox3.AppendText(&quot;3&quot;)
            txtDataReceived.Clear()

        ElseIf txtDataReceived.Text = &quot;4&quot; Then
            Button13.Select()
            Dim c As Integer
            Dim d As Integer
            Dim ProcID As Integer
            'Dim c As Integer
            'Dim d As Integer
            ProcID = Shell(&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;, AppWinStyle.NormalFocus)
            ' c = &quot;0&quot;
            'My.Forms.Form1.Button10.    
            TextBox2.Text = &quot;0&quot;
            'Me.TopMost = True
            'ProcID = Form1.TextBox2.Text
            Form1a.TextBox1.Text = ProcID
            TextBox1.Text = Form1a.TextBox1.Text
            'MsgBox(ProcID)
            'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
            ProcID = Form1a.TextBox1.Text
            ' ProcID = &quot;Windows Media Player&quot;
            'TextBox1.Text = ProcID
            ' On Error GoTo errorhandler
            c = TextBox1.Text
            'TextBox1.Text = Form1.TextBox1.Text
            TextBox2.Text = Form1a.TextBox3.Text
            AppActivate(&quot;Windows Media Player&quot;)

            My.Computer.Keyboard.SendKeys(&quot;%S&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;%FOn&quot;, True)
            'AppActivate(&quot;Open&quot;)
            My.Computer.Keyboard.SendKeys(&quot;%n&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;4.wma&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;%P&quot;, True)
            TextBox3.AppendText(&quot;4&quot;)
            txtDataReceived.Clear()
        ElseIf txtDataReceived.Text = &quot;5&quot; Then
            Button14.Select()
            Dim c As Integer
            Dim d As Integer
            Dim ProcID As Integer
            'Dim c As Integer
            'Dim d As Integer
            ProcID = Shell(&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;, AppWinStyle.NormalFocus)
            ' c = &quot;0&quot;
            'My.Forms.Form1.Button10.    
            TextBox2.Text = &quot;0&quot;
            'Me.TopMost = True
            'ProcID = Form1.TextBox2.Text
            Form1a.TextBox1.Text = ProcID
            TextBox1.Text = Form1a.TextBox1.Text
            'MsgBox(ProcID)
            'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
            ProcID = Form1a.TextBox1.Text
            ' ProcID = &quot;Windows Media Player&quot;
            'TextBox1.Text = ProcID
            ' On Error GoTo errorhandler
            c = TextBox1.Text
            'TextBox1.Text = Form1.TextBox1.Text
            TextBox2.Text = Form1a.TextBox3.Text
            AppActivate(&quot;Windows Media Player&quot;)

            My.Computer.Keyboard.SendKeys(&quot;%S&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;%FOn&quot;, True)
            'AppActivate(&quot;Open&quot;)
            My.Computer.Keyboard.SendKeys(&quot;%n&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;5.wma&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;%P&quot;, True)
            TextBox3.AppendText(&quot;5&quot;)
            txtDataReceived.Clear()
        ElseIf txtDataReceived.Text = &quot;6&quot; Then
            Button15.Select()
            Dim c As Integer
            Dim d As Integer
            Dim ProcID As Integer
            'Dim c As Integer
            'Dim d As Integer
            ProcID = Shell(&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;, AppWinStyle.NormalFocus)
            ' c = &quot;0&quot;
            'My.Forms.Form1.Button10.    
            TextBox2.Text = &quot;0&quot;
            'Me.TopMost = True
            'ProcID = Form1.TextBox2.Text
            Form1a.TextBox1.Text = ProcID
            TextBox1.Text = Form1a.TextBox1.Text
            'MsgBox(ProcID)
            'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
            ProcID = Form1a.TextBox1.Text
            ' ProcID = &quot;Windows Media Player&quot;
            'TextBox1.Text = ProcID
            ' On Error GoTo errorhandler
            c = TextBox1.Text
            'TextBox1.Text = Form1.TextBox1.Text
            TextBox2.Text = Form1a.TextBox3.Text
            AppActivate(&quot;Windows Media Player&quot;)

            My.Computer.Keyboard.SendKeys(&quot;%S&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;%FOn&quot;, True)
            'AppActivate(&quot;Open&quot;)
            My.Computer.Keyboard.SendKeys(&quot;%n&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;6.wma&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;%P&quot;, True)
            TextBox3.AppendText(&quot;6&quot;)
            txtDataReceived.Clear()
        ElseIf txtDataReceived.Text = &quot;7&quot; Then
            Button16.Select()
            Dim c As Integer
            Dim d As Integer
            Dim ProcID As Integer
            'Dim c As Integer
            'Dim d As Integer
            ProcID = Shell(&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;, AppWinStyle.NormalFocus)
            ' c = &quot;0&quot;
            'My.Forms.Form1.Button10.    
            TextBox2.Text = &quot;0&quot;
            'Me.TopMost = True
            'ProcID = Form1.TextBox2.Text
            Form1a.TextBox1.Text = ProcID
            TextBox1.Text = Form1a.TextBox1.Text
            'MsgBox(ProcID)
            'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
            ProcID = Form1a.TextBox1.Text
            ' ProcID = &quot;Windows Media Player&quot;
            'TextBox1.Text = ProcID
            ' On Error GoTo errorhandler
            c = TextBox1.Text
            'TextBox1.Text = Form1.TextBox1.Text
            TextBox2.Text = Form1a.TextBox3.Text
            AppActivate(&quot;Windows Media Player&quot;)

            My.Computer.Keyboard.SendKeys(&quot;%S&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;%FOn&quot;, True)
            'AppActivate(&quot;Open&quot;)
            My.Computer.Keyboard.SendKeys(&quot;%n&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;7.wma&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;%P&quot;, True)
            TextBox3.AppendText(&quot;7&quot;)
            txtDataReceived.Clear()
        ElseIf txtDataReceived.Text = &quot;8&quot; Then
            Button17.Select()
            Dim c As Integer
            Dim d As Integer
            Dim ProcID As Integer
            'Dim c As Integer
            'Dim d As Integer
            ProcID = Shell(&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;, AppWinStyle.NormalFocus)
            ' c = &quot;0&quot;
            'My.Forms.Form1.Button10.    
            TextBox2.Text = &quot;0&quot;
            'Me.TopMost = True
            'ProcID = Form1.TextBox2.Text
            Form1a.TextBox1.Text = ProcID
            TextBox1.Text = Form1a.TextBox1.Text
            'MsgBox(ProcID)
            'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
            ProcID = Form1a.TextBox1.Text
            ' ProcID = &quot;Windows Media Player&quot;
            'TextBox1.Text = ProcID
            ' On Error GoTo errorhandler
            c = TextBox1.Text
            'TextBox1.Text = Form1.TextBox1.Text
            TextBox2.Text = Form1a.TextBox3.Text
            AppActivate(&quot;Windows Media Player&quot;)

            My.Computer.Keyboard.SendKeys(&quot;%S&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;%FOn&quot;, True)
            'AppActivate(&quot;Open&quot;)
            My.Computer.Keyboard.SendKeys(&quot;%n&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;8.wma&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;%P&quot;, True)
            TextBox3.AppendText(&quot;8&quot;)
            txtDataReceived.Clear()
        ElseIf txtDataReceived.Text = &quot;9&quot; Then
            Button18.Select()
            Dim c As Integer
            Dim d As Integer
            Dim ProcID As Integer
            'Dim c As Integer
            'Dim d As Integer
            ProcID = Shell(&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;, AppWinStyle.NormalFocus)
            ' c = &quot;0&quot;
            'My.Forms.Form1.Button10.    
            TextBox2.Text = &quot;0&quot;
            'Me.TopMost = True
            'ProcID = Form1.TextBox2.Text
            Form1a.TextBox1.Text = ProcID
            TextBox1.Text = Form1a.TextBox1.Text
            'MsgBox(ProcID)
            'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
            ProcID = Form1a.TextBox1.Text
            ' ProcID = &quot;Windows Media Player&quot;
            'TextBox1.Text = ProcID
            ' On Error GoTo errorhandler
            c = TextBox1.Text
            'TextBox1.Text = Form1.TextBox1.Text
            TextBox2.Text = Form1a.TextBox3.Text
            AppActivate(&quot;Windows Media Player&quot;)

            My.Computer.Keyboard.SendKeys(&quot;%S&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;%FOn&quot;, True)
            'AppActivate(&quot;Open&quot;)
            My.Computer.Keyboard.SendKeys(&quot;%n&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;9.wma&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;%P&quot;, True)
            TextBox3.AppendText(&quot;9&quot;)
            txtDataReceived.Clear()
        ElseIf txtDataReceived.Text = &quot;0&quot; Then
            Button19.Select()
            Dim c As Integer
            Dim d As Integer
            Dim ProcID As Integer
            'Dim c As Integer
            'Dim d As Integer
            ProcID = Shell(&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;, AppWinStyle.NormalFocus)
            ' c = &quot;0&quot;
            'My.Forms.Form1.Button10.    
            TextBox2.Text = &quot;0&quot;
            'Me.TopMost = True
            'ProcID = Form1.TextBox2.Text
            Form1a.TextBox1.Text = ProcID
            TextBox1.Text = Form1a.TextBox1.Text
            'MsgBox(ProcID)
            'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
            ProcID = Form1a.TextBox1.Text
            ' ProcID = &quot;Windows Media Player&quot;
            'TextBox1.Text = ProcID
            ' On Error GoTo errorhandler
            c = TextBox1.Text
            'TextBox1.Text = Form1.TextBox1.Text
            TextBox2.Text = Form1a.TextBox3.Text
            AppActivate(&quot;Windows Media Player&quot;)

            My.Computer.Keyboard.SendKeys(&quot;%S&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;%FOn&quot;, True)
            'AppActivate(&quot;Open&quot;)
            My.Computer.Keyboard.SendKeys(&quot;%n&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;0.wma&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;%P&quot;, True)
            TextBox3.AppendText(&quot;0&quot;)
            txtDataReceived.Clear()
        ElseIf txtDataReceived.Text = &quot;b&quot; Then
            Button20.Select()
            Dim c As Integer
            Dim d As Integer
            Dim ProcID As Integer
            'Dim c As Integer
            'Dim d As Integer
            ProcID = Shell(&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;, AppWinStyle.NormalFocus)
            ' c = &quot;0&quot;
            'My.Forms.Form1.Button10.    
            TextBox2.Text = &quot;0&quot;
            'Me.TopMost = True
            'ProcID = Form1.TextBox2.Text
            Form1a.TextBox1.Text = ProcID
            TextBox1.Text = Form1a.TextBox1.Text
            'MsgBox(ProcID)
            'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
            ProcID = Form1a.TextBox1.Text
            ' ProcID = &quot;Windows Media Player&quot;
            'TextBox1.Text = ProcID
            ' On Error GoTo errorhandler
            c = TextBox1.Text
            'TextBox1.Text = Form1.TextBox1.Text
            TextBox2.Text = Form1a.TextBox3.Text
            AppActivate(&quot;Windows Media Player&quot;)

            My.Computer.Keyboard.SendKeys(&quot;%S&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;%FOn&quot;, True)
            'AppActivate(&quot;Open&quot;)
            My.Computer.Keyboard.SendKeys(&quot;%n&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;star.wma&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;%P&quot;, True)
            TextBox3.AppendText(&quot;*&quot;)
            txtDataReceived.Clear()
        ElseIf txtDataReceived.Text = &quot;a&quot; Then
            Button21.Select()
            Dim c As Integer
            Dim d As Integer
            Dim ProcID As Integer
            'Dim c As Integer
            'Dim d As Integer
            ProcID = Shell(&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;, AppWinStyle.NormalFocus)
            ' c = &quot;0&quot;
            'My.Forms.Form1.Button10.    
            TextBox2.Text = &quot;0&quot;
            'Me.TopMost = True
            'ProcID = Form1.TextBox2.Text
            Form1a.TextBox1.Text = ProcID
            TextBox1.Text = Form1a.TextBox1.Text
            'MsgBox(ProcID)
            'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
            ProcID = Form1a.TextBox1.Text
            ' ProcID = &quot;Windows Media Player&quot;
            'TextBox1.Text = ProcID
            ' On Error GoTo errorhandler
            c = TextBox1.Text
            'TextBox1.Text = Form1.TextBox1.Text
            TextBox2.Text = Form1a.TextBox3.Text
            AppActivate(&quot;Windows Media Player&quot;)

            My.Computer.Keyboard.SendKeys(&quot;%S&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;%FOn&quot;, True)
            'AppActivate(&quot;Open&quot;)
            My.Computer.Keyboard.SendKeys(&quot;%n&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;has.wma&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
            My.Computer.Keyboard.SendKeys(&quot;%P&quot;, True)
            TextBox3.AppendText(&quot;#&quot;)
            txtDataReceived.Clear()
        ElseIf txtDataReceived.Text = &quot;&#43;&quot; Then
            ' txtDataReceived.AppendText(&quot;0&quot;)
            '  MsgBox(&quot;&#43;&quot;)
            Button23.PerformClick()
            '  ElseIf txtDataReceived.Text = &quot;&#43;&quot; Then 'And txtDataReceived.Text = &quot;&#43;&quot; Then
            Button27.PerformClick()
            txtDataReceived.Clear()
            TextBox5.Clear()
            '  Button24.PerformClick()
            'ElseIf txtDataReceived.Text = &quot;!P&quot; Then
        ElseIf txtDataReceived.Text = &quot;#&quot; Then
            '  txtDataReceived.AppendText(&quot;1&quot;)
            Button26.PerformClick()

            '   btnSendData.PerformClick()
            '  btnSendData.PerformClick()
            ' btnSendData.PerformClick()
            ' btnSendData.PerformClick()
            ' btnSendData.PerformClick()
            ' btnSendData.PerformClick()
            ' btnSendData.PerformClick()
            ' btnSendData.PerformClick()
            Button25.PerformClick()
            txtDataReceived.Clear()
            TextBox5.Clear()
        ElseIf txtDataReceived.Text = &quot;s&quot; Then
            '  txtDataReceived.AppendText(&quot;2&quot;)
            Button11.PerformClick()
        ElseIf txtDataReceived.Text = &quot;t&quot; Then
            '    txtDataReceived.AppendText(&quot;3&quot;)
            Button12.PerformClick()
        ElseIf txtDataReceived.Text = &quot;u&quot; Then
            '   txtDataReceived.AppendText(&quot;4&quot;)
            Button13.PerformClick()
        ElseIf txtDataReceived.Text = &quot;v&quot; Then
            '   txtDataReceived.AppendText(&quot;5&quot;)
            Button14.PerformClick()
        ElseIf txtDataReceived.Text = &quot;w&quot; Then
            '   txtDataReceived.AppendText(&quot;6&quot;)
            Button15.PerformClick()
        ElseIf txtDataReceived.Text = &quot;x&quot; Then
            '   txtDataReceived.AppendText(&quot;7&quot;)
            Button16.PerformClick()
        ElseIf txtDataReceived.Text = &quot;y&quot; Then
            '   txtDataReceived.AppendText(&quot;8&quot;)
            Button17.PerformClick()
        ElseIf txtDataReceived.Text = &quot;p&quot; Then
            '   txtDataReceived.AppendText(&quot;9&quot;)
            Button18.PerformClick()
            '     ElseIf Keys.NumPad6 Then
            '         txtDataReceived.Text = &quot;6&quot;
        ElseIf TextBox5.Text = &quot;P&quot; Then
            TextBox5.Clear()
            '  Else : TextBox5.Clear()
        ElseIf TextBox5.Text = &quot;#&quot; Then
            TextBox5.Clear()
        ElseIf TextBox5.Text = &quot;!&quot; Then
            TextBox5.Clear()
        ElseIf TextBox5.Text = &quot;!#P&quot; Then
            TextBox5.Clear()
        End If
        '  TextBox5.Clear()
        ' End If
    End Sub

    Private Sub TextBox1_TextChanged(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles txtDataReceivedd.TextChanged

    End Sub

    Private Sub txtData_TextChanged(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles txtData.TextChanged
        TextBox1.Text = txtData.Text
    End Sub

    Private Sub TextBox1_TextChanged_1(ByVal sender As System.Object, ByVal e As System.EventArgs)

    End Sub

    Private Sub Button1_Click(ByVal sender As Object, _
        ByVal e As System.EventArgs) Handles Button1.Click
        Dim psi As New  _
            System.Diagnostics.ProcessStartInfo(&quot;C:\windows\system32\calc.exe&quot;)
        psi.RedirectStandardOutput = True
        psi.WindowStyle = ProcessWindowStyle.Hidden
        psi.UseShellExecute = False
        Dim listFiles As System.Diagnostics.Process
        listFiles = System.Diagnostics.Process.Start(psi)
        Dim myOutput As System.IO.StreamReader _
            = listFiles.StandardOutput
        listFiles.WaitForExit(2000)
        If listFiles.HasExited Then
            Dim output As String = myOutput.ReadToEnd
            Debug.WriteLine(output)
        End If
    End Sub

    Private Sub Button2_Click(sender As System.Object, e As System.EventArgs) Handles Button2.Click
        Dim Filename As String
        Dim Res As String
        Dim sData As Integer

        Dim sNWind As String
        Dim a As Byte


        Dim a1 As Integer
        'On Error Resume Next
        '   &quot;C:\Users\House\Desktop\a.txt&quot;


        Res = Shell(Chr(34) &amp; &quot;C:\Windows\System32\calc.exe&quot;, vbMaximizedFocus)
        ' Print(&quot;C:\Windows\System32\calc.exe&quot;)
        Res = (a1)

        Print(Shell(Chr(34) &amp; &quot;C:\Users\House\Desktop\a.txt&quot; &amp; Chr(34)), a1)
        'Close the connection
        'rs.Close()
        '  conn.Close()





        Filename = &quot;C:\windows\system32\calc.exe&quot; 'Check file is here first


        If Dir(Filename) = &quot;&quot; Then
            MsgBox(Filename &amp; &quot; not found&quot;, vbInformation)
        Else
            'Res = Shell(&quot;Calculator.exe &quot; &amp; Filename, vbHide)
            Res = Shell(&quot;C:\Users\House\Desktop\VB.net 2005 Simple CDC Demo &quot; &amp; _
  txtData.Text, vbMaximizedFocus)
            Button3.Enabled = True
            Button3_Click()

        End If

    End Sub

    Private Sub Button3_Click() Handles Button3.Click
        Dim Res As String

        Res = Shell(&quot;C:\Users\House\Desktop\VB.net 2005 Simple CDC Demo &quot; &amp; _
  txtData.Text, vbMaximizedFocus)
    End Sub

    Private Function KeyPressEventArgs() As Type
        On Error Resume Next
        Throw New ApplicationException
        ' Code to react to possible causes of the exception.

    End Function

    Private Function b1() As String
        Throw New NotImplementedException
    End Function

    Private Sub Button4_Click(sender As System.Object, e As System.EventArgs) Handles Button4.Click
        Dim oExcel As Object
        Dim oBook As Object
        Dim oSheet As Object
        Dim oCalc As Object

        'Start a new workbook in Excel
        'oCalc = CreateObject(&quot;C:\windows\system32\calc.exe&quot;)
        oExcel = CreateObject(&quot;Excel.Application&quot;)
        oBook = oExcel.Workbooks.Add


        'Add data to cells of the first worksheet in the new workbook
        oSheet = oBook.Worksheets(1)
        oSheet.Range(&quot;A1&quot;).Value = &quot;Last Name&quot;
        oSheet.Range(&quot;B1&quot;).Value = &quot;First Name&quot;
        oSheet.Range(&quot;A1:B1&quot;).Font.Bold = True
        oSheet.Range(&quot;A2&quot;).Value = &quot;Doe&quot;
        oSheet.Range(&quot;B2&quot;).Value = &quot;John&quot;

        'Save the Workbook and Quit Excel
        oBook.SaveAs(&quot;C:\Book1.xls&quot;)
        oExcel.Quit()
    End Sub

    Private Sub Button5_Click(sender As System.Object, e As System.EventArgs) Handles Button5.Click
        'Create a new connection object for Book1.xls
        TextBox1.Text = txtData.Text

    End Sub

    Private Sub TextBox1_TextChanged_2(sender As System.Object, e As System.EventArgs) Handles TextBox1.TextChanged

    End Sub

    Private Sub Form1_Load(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles MyBase.Load
        Dim i As Integer
        ' Create a timer with a ten second interval.
        aTimer = New System.Timers.Timer(10000)
        aTimer.Interval = 2000
        aTimer.Enabled = True
        ' Hook up the Elapsed event for the timer. 
        AddHandler aTimer.Elapsed, AddressOf OnTimedEvent

        ' Set the Interval to 2 seconds (2000 milliseconds).
       
   
        'Console.WriteLine(&quot;Press the Enter key to exit the program.&quot;)
        ' Console.ReadLine()
    End Sub

    Private Sub Button6_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button6.Click
        Form1a.Show()
    End Sub

    Private Sub Button7_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button7.Click

    End Sub

    Private Sub Button8_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button8.Click
        Form1a.TextBox3.Text = txtDataReceived.Text
        Form1a.TextBox3.Text = TextBox3.Text
        Form1a.TextBox1.Text = Skype.TextBox1.Text
        'Form2.TextBox2.text = txtDataReceived.Text
    End Sub

    Private Sub Button9_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button9.Click
        Dim ProcID As Integer
        Dim a As Integer
        Dim c As Integer
        'Dim d1 As String
        Dim e1a As Integer
        ' Start the Calculator application, and store the process id.
        ' On Error GoTo errorhandler
        'GoTo Pause
        ''Form2.Show()
        'ProcID = Shell(&quot;C:\Program Files\Microsoft Office\Office14\Excel.exe&quot;, AppWinStyle.NormalFocus)
        'Test.Main1()
        DirAppend.Main()
        'List''x1.Items.Add()
        ''ProcID = Shell(&quot;C:\Program Files\Microsoft Office\Office14\Excel.exe&quot;, AppWinStyle.NormalFocus)
        ''MsgBox(ProcID)
        ' Skype.Show()
        ' Skype.TopMost = True
        'TextBox3.Text = ListBox1.SelectedItem
        ' If Skype.TextBox1.Text = TextBox1.Text Then
        'Skype.Show()
        '   End If

        ' c = &quot;0&quot;
        'TextBox2.Text = &quot;0&quot;


        'ProcID = Form1.TextBox2.Text
        ''TextBox1.Text = ProcID
        'TextBox1.Text = Form1.TextBox1.Text
        '  MsgBox(ProcID)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' ProcI''D = 'Form1.TextBox1.Text
        'TextBox1.Text = ProcID
        ''c = TextBox1.Text
        'TextBox1.Text = Form1.TextBox1.Text
        ' TextBox2.Text = Form1.TextBox3.Text
        ''MsgBox(c)
        ''AppActivate(c)

        'My.Computer.Keyboard.SendKeys(&quot;123qweasdzxc&quot;, True)
        ''My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;%c&quot;, True)
        'My.Computer.Keyboard.SendKe'ys(&quot;~&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;123qweasdzxc&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;%FO&quot;, True)
        ''My.Computer.Keyboard.SendKeys(&quot;%F&quot;, True)
        ''My.Computer.Keyboard.SendKeys(&quot;{TAB}&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;PhoneBook.txt&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;PhoneBook.txt&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;{TAB}&quot;, True)
        ''My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;PhoneBook.txt&quot;, True)
        ''My.Computer.Keyboard.SendKeys(&quot;%F&quot;, True)
        ''My.Computer.Keyboard.SendKeys(&quot;{TAB}&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;{TAB}&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;{TAB}&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;&#43;O&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;&#43;N&quot;, True)

        'My.Computer.Keyboard.SendKeys(&quot;&#43;N&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;&#43;F&quot;, True)
        'My.Computer.Keyb'oard.SendKeys(&quot;{TAB}&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;{TAB}&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ''My.Computer.Keyboard.SendKeys(&quot;^C&quot;, True)
        ''My.Computer.Keyboard.SendKeys(&quot;^c&quot;, True)
        ''My.Computer.Keyboard.SendKeys(&quot;^c&quot;, True)
        ''My.Computer.Keyboard.SendKeys(&quot;^c&quot;, True)
        ''My.Computer.Keyboard.SendKeys(&quot;^c&quot;, True)
        ''My.Computer.Keyboard.SendKeys(&quot;^c&quot;, True)
        'Me.Top = False
        ''Me.Show()
        ''Me.Select()
        ''txtDataReceived.Clear()
        ''txtDataReceived.Paste()
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' Me.Show()
        ' My.Computer.Keyboard.SendKeys(&quot;006583642487&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        'My.Computer.Keyboard.SendKeys(d, True)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;%&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;%al&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;%F&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;006591737839&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        'Else

        '  End If
        'GoTo Pause
        ''Form2.TopMost() = True
        'ProcID = Shell(&quot;C:\Program Files\Voxox\Vovox.EXE&quot;, AppWinStyle.NormalFocus)


errorhandler:
        Exit Sub
    End Sub

    Private Sub ListBox1_SelectedIndexChanged(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles ListBox1.SelectedIndexChanged
        txtDataReceived.Text = ListBox1.SelectedItem
        TextBox3.Text = ListBox1.SelectedItem
    End Sub

    '  Imports System
    'Imports System.IO
    'Users1\WindowsHome\Documents\
    Class DirAppend
        Public Shared Sub Main()
            Using w As StreamWriter = File.AppendText(&quot;F:\PhoneBook.txt&quot;)
                Log(&quot;Test1&quot;, w)
                Log(&quot;Test2&quot;, w)
            End Using
            'Users1\WindowsHome\Documents\
            Using r As StreamReader = File.OpenText(&quot;F:\PhoneBook.txt&quot;)
                DumpLog(r)
            End Using
        End Sub

        Public Shared Sub Log(ByVal logMessage As String, ByVal w As TextWriter)
            w.Write(vbCrLf &#43; &quot;Log Entry : &quot;)
            w.WriteLine(&quot;{0} {1}&quot;, DateTime.Now.ToLongTimeString(), _
                DateTime.Now.ToLongDateString())
            w.WriteLine(&quot;  :&quot;)
            w.WriteLine(&quot;  :{0}&quot;, logMessage)
            w.WriteLine(&quot;-------------------------------&quot;)
        End Sub

        Public Shared Sub DumpLog(ByVal r As StreamReader)
            On Error GoTo errorhandler
            Dim line As String
            Dim i As Integer
            For i = 1 To 100
                line = r.ReadLine()
                My.Forms.Form1.ListBox1.Items.Add(line)
            Next i
            While Not (line Is Nothing)
                Console.WriteLine(line)
                line = r.ReadLine()
                '   My.Forms.Form1.ListBox1.Items.Add(line)
            End While
errorhandler:
            Exit Sub
        End Sub
    End Class


    Sub Button10_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button10.Click
        Dim c As Integer
        Dim d As Integer
        Dim ProcID As Integer
        'Dim c As Integer
        'Dim d As Integer
        ProcID = Shell(&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;, AppWinStyle.NormalFocus)
        ' c = &quot;0&quot;
        'My.Forms.Form1.Button10.    
        TextBox2.Text = &quot;0&quot;
        'Me.TopMost = True
        'ProcID = Form1.TextBox2.Text
        Form1a.TextBox1.Text = ProcID
        TextBox1.Text = Form1a.TextBox1.Text
        'MsgBox(ProcID)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ProcID = Form1a.TextBox1.Text
        ' ProcID = &quot;Windows Media Player&quot;
        'TextBox1.Text = ProcID
        ' On Error GoTo errorhandler
        c = TextBox1.Text
        'TextBox1.Text = Form1.TextBox1.Text
        TextBox2.Text = Form1a.TextBox3.Text
        AppActivate(&quot;Windows Media Player&quot;)

        My.Computer.Keyboard.SendKeys(&quot;%S&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%FOn&quot;, True)
        'AppActivate(&quot;Open&quot;)
        My.Computer.Keyboard.SendKeys(&quot;%n&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;1.wma&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%P&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;P&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        '' My.Computer.Keyboard.SendKeys(&quot;^P&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;006591737839&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        txtDataReceived.AppendText(&quot;1&quot;)
    End Sub

    Private Sub Button11_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button11.Click
        Dim c As Integer
        Dim d As Integer
        Dim ProcID As Integer
        'Dim c As Integer
        'Dim d As Integer
        ProcID = Shell(&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;, AppWinStyle.NormalFocus)
        ' c = &quot;0&quot;
        TextBox2.Text = &quot;0&quot;
        'Me.TopMost = True
        'ProcID = Form1.TextBox2.Text
        Form1a.TextBox1.Text = ProcID
        TextBox1.Text = Form1a.TextBox1.Text
        'MsgBox(ProcID)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ProcID = Form1a.TextBox1.Text
        ' ProcID = &quot;Windows Media Player&quot;
        'TextBox1.Text = ProcID
        ' On Error GoTo errorhandler
        c = TextBox1.Text
        'TextBox1.Text = Form1.TextBox1.Text
        TextBox2.Text = Form1a.TextBox3.Text
        AppActivate(&quot;Windows Media Player&quot;)

        My.Computer.Keyboard.SendKeys(&quot;%S&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%FOn&quot;, True)
        'AppActivate(&quot;Open&quot;)
        My.Computer.Keyboard.SendKeys(&quot;%n&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;2.wma&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%P&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;P&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        '' My.Computer.Keyboard.SendKeys(&quot;^P&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;006591737839&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        txtDataReceived.AppendText(&quot;2&quot;)
    End Sub

    Private Sub Button12_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button12.Click
        Dim c As Integer
        Dim d As Integer
        Dim ProcID As Integer
        'Dim c As Integer
        'Dim d As Integer
        ProcID = Shell(&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;, AppWinStyle.NormalFocus)
        ' c = &quot;0&quot;
        TextBox2.Text = &quot;0&quot;
        'Me.TopMost = True
        'ProcID = Form1.TextBox2.Text
        Form1a.TextBox1.Text = ProcID
        TextBox1.Text = Form1a.TextBox1.Text
        'MsgBox(ProcID)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ProcID = Form1a.TextBox1.Text
        ' ProcID = &quot;Windows Media Player&quot;
        'TextBox1.Text = ProcID
        ' On Error GoTo errorhandler
        c = TextBox1.Text
        'TextBox1.Text = Form1.TextBox1.Text
        TextBox2.Text = Form1a.TextBox3.Text
        AppActivate(&quot;Windows Media Player&quot;)

        My.Computer.Keyboard.SendKeys(&quot;%S&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%FOn&quot;, True)
        'AppActivate(&quot;Open&quot;)
        My.Computer.Keyboard.SendKeys(&quot;%n&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;3.wma&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%P&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;P&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        '' My.Computer.Keyboard.SendKeys(&quot;^P&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;006591737839&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        txtDataReceived.AppendText(&quot;3&quot;)
    End Sub

    Private Sub Button13_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button13.Click
        Dim c As Integer
        Dim d As Integer
        Dim ProcID As Integer
        'Dim c As Integer
        'Dim d As Integer
        ProcID = Shell(&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;, AppWinStyle.NormalFocus)
        ' c = &quot;0&quot;
        TextBox2.Text = &quot;0&quot;
        'Me.TopMost = True
        'ProcID = Form1.TextBox2.Text
        Form1a.TextBox1.Text = ProcID
        TextBox1.Text = Form1a.TextBox1.Text
        'MsgBox(ProcID)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ProcID = Form1a.TextBox1.Text
        ' ProcID = &quot;Windows Media Player&quot;
        'TextBox1.Text = ProcID
        ' On Error GoTo errorhandler
        c = TextBox1.Text
        'TextBox1.Text = Form1.TextBox1.Text
        TextBox2.Text = Form1a.TextBox3.Text
        AppActivate(&quot;Windows Media Player&quot;)

        My.Computer.Keyboard.SendKeys(&quot;%S&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%FOn&quot;, True)
        'AppActivate(&quot;Open&quot;)
        My.Computer.Keyboard.SendKeys(&quot;%n&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;4.wma&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%P&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;P&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        '' My.Computer.Keyboard.SendKeys(&quot;^P&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;006591737839&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        txtDataReceived.AppendText(&quot;4&quot;)
    End Sub

    Private Sub Button14_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button14.Click
        Dim c As Integer
        Dim d As Integer
        Dim ProcID As Integer
        'Dim c As Integer
        'Dim d As Integer
        ProcID = Shell(&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;, AppWinStyle.NormalFocus)
        ' c = &quot;0&quot;
        TextBox2.Text = &quot;0&quot;
        'Me.TopMost = True
        'ProcID = Form1.TextBox2.Text
        Form1a.TextBox1.Text = ProcID
        TextBox1.Text = Form1a.TextBox1.Text
        'MsgBox(ProcID)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ProcID = Form1a.TextBox1.Text
        ' ProcID = &quot;Windows Media Player&quot;
        'TextBox1.Text = ProcID
        ' On Error GoTo errorhandler
        c = TextBox1.Text
        'TextBox1.Text = Form1.TextBox1.Text
        TextBox2.Text = Form1a.TextBox3.Text
        AppActivate(&quot;Windows Media Player&quot;)

        My.Computer.Keyboard.SendKeys(&quot;%S&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%FOn&quot;, True)
        'AppActivate(&quot;Open&quot;)
        My.Computer.Keyboard.SendKeys(&quot;%n&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;5.wma&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%P&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;P&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        '' My.Computer.Keyboard.SendKeys(&quot;^P&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;006591737839&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        txtDataReceived.AppendText(&quot;5&quot;)
    End Sub

    Private Sub Button15_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button15.Click
        Dim c As Integer
        Dim d As Integer
        Dim ProcID As Integer
        'Dim c As Integer
        'Dim d As Integer
        ProcID = Shell(&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;, AppWinStyle.NormalFocus)
        ' c = &quot;0&quot;
        TextBox2.Text = &quot;0&quot;
        'Me.TopMost = True
        'ProcID = Form1.TextBox2.Text
        Form1a.TextBox1.Text = ProcID
        TextBox1.Text = Form1a.TextBox1.Text
        'MsgBox(ProcID)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ProcID = Form1a.TextBox1.Text
        ' ProcID = &quot;Windows Media Player&quot;
        'TextBox1.Text = ProcID
        ' On Error GoTo errorhandler
        c = TextBox1.Text
        'TextBox1.Text = Form1.TextBox1.Text
        TextBox2.Text = Form1a.TextBox3.Text
        AppActivate(&quot;Windows Media Player&quot;)

        My.Computer.Keyboard.SendKeys(&quot;%S&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%FOn&quot;, True)
        'AppActivate(&quot;Open&quot;)
        My.Computer.Keyboard.SendKeys(&quot;%n&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;6.wma&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%P&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;P&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        '' My.Computer.Keyboard.SendKeys(&quot;^P&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;006591737839&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        txtDataReceived.AppendText(&quot;6&quot;)
    End Sub

    Private Sub Button16_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button16.Click
        Dim c As Integer
        Dim d As Integer
        Dim ProcID As Integer
        'Dim c As Integer
        'Dim d As Integer
        ProcID = Shell(&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;, AppWinStyle.NormalFocus)
        ' c = &quot;0&quot;
        TextBox2.Text = &quot;0&quot;
        'Me.TopMost = True
        'ProcID = Form1.TextBox2.Text
        Form1a.TextBox1.Text = ProcID
        TextBox1.Text = Form1a.TextBox1.Text
        'MsgBox(ProcID)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ProcID = Form1a.TextBox1.Text
        ' ProcID = &quot;Windows Media Player&quot;
        'TextBox1.Text = ProcID
        ' On Error GoTo errorhandler
        c = TextBox1.Text
        'TextBox1.Text = Form1.TextBox1.Text
        TextBox2.Text = Form1a.TextBox3.Text
        AppActivate(&quot;Windows Media Player&quot;)

        My.Computer.Keyboard.SendKeys(&quot;%S&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%FOn&quot;, True)
        'AppActivate(&quot;Open&quot;)
        My.Computer.Keyboard.SendKeys(&quot;%n&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;7.wma&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%P&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;P&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        '' My.Computer.Keyboard.SendKeys(&quot;^P&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;006591737839&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        txtDataReceived.AppendText(&quot;7&quot;)
    End Sub

    Private Sub Button17_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button17.Click
        Dim c As Integer
        Dim d As Integer
        Dim ProcID As Integer
        'Dim c As Integer
        'Dim d As Integer
        ProcID = Shell(&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;, AppWinStyle.NormalFocus)
        ' c = &quot;0&quot;
        TextBox2.Text = &quot;0&quot;
        'Me.TopMost = True
        'ProcID = Form1.TextBox2.Text
        Form1a.TextBox1.Text = ProcID
        TextBox1.Text = Form1a.TextBox1.Text
        'MsgBox(ProcID)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ProcID = Form1a.TextBox1.Text
        ' ProcID = &quot;Windows Media Player&quot;
        'TextBox1.Text = ProcID
        ' On Error GoTo errorhandler
        c = TextBox1.Text
        'TextBox1.Text = Form1.TextBox1.Text
        TextBox2.Text = Form1a.TextBox3.Text
        AppActivate(&quot;Windows Media Player&quot;)

        My.Computer.Keyboard.SendKeys(&quot;%S&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%FOn&quot;, True)
        'AppActivate(&quot;Open&quot;)
        My.Computer.Keyboard.SendKeys(&quot;%n&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;8.wma&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%P&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;P&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        '' My.Computer.Keyboard.SendKeys(&quot;^P&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;006591737839&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        txtDataReceived.AppendText(&quot;8&quot;)
    End Sub

    Private Sub Button18_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button18.Click
        Dim c As Integer
        Dim d As Integer
        Dim ProcID As Integer
        'Dim c As Integer
        'Dim d As Integer
        ProcID = Shell(&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;, AppWinStyle.NormalFocus)
        ' c = &quot;0&quot;
        TextBox2.Text = &quot;0&quot;
        'Me.TopMost = True
        'ProcID = Form1.TextBox2.Text
        Form1a.TextBox1.Text = ProcID
        TextBox1.Text = Form1a.TextBox1.Text
        'MsgBox(ProcID)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ProcID = Form1a.TextBox1.Text
        ' ProcID = &quot;Windows Media Player&quot;
        'TextBox1.Text = ProcID
        ' On Error GoTo errorhandler
        c = TextBox1.Text
        'TextBox1.Text = Form1.TextBox1.Text
        TextBox2.Text = Form1a.TextBox3.Text
        AppActivate(&quot;Windows Media Player&quot;)

        My.Computer.Keyboard.SendKeys(&quot;%S&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%FOn&quot;, True)
        'AppActivate(&quot;Open&quot;)
        My.Computer.Keyboard.SendKeys(&quot;%n&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;9.wma&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%P&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;P&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        '' My.Computer.Keyboard.SendKeys(&quot;^P&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;006591737839&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        txtDataReceived.AppendText(&quot;9&quot;)
    End Sub

    Private Sub Button19_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button19.Click
        Dim c As Integer
        Dim d As Integer
        Dim ProcID As Integer
        'Dim c As Integer
        'Dim d As Integer
        ProcID = Shell(&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;, AppWinStyle.NormalFocus)
        ' c = &quot;0&quot;
        TextBox2.Text = &quot;0&quot;
        'Me.TopMost = True
        'ProcID = Form1.TextBox2.Text
        Form1a.TextBox1.Text = ProcID
        TextBox1.Text = Form1a.TextBox1.Text
        'MsgBox(ProcID)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ProcID = Form1a.TextBox1.Text
        ' ProcID = &quot;Windows Media Player&quot;
        'TextBox1.Text = ProcID
        ' On Error GoTo errorhandler
        c = TextBox1.Text
        'TextBox1.Text = Form1.TextBox1.Text
        TextBox2.Text = Form1a.TextBox3.Text
        AppActivate(&quot;Windows Media Player&quot;)
        txtDataReceived.AppendText(&quot;0&quot;)
        My.Computer.Keyboard.SendKeys(&quot;%S&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%FOn&quot;, True)
        'AppActivate(&quot;Open&quot;)
        My.Computer.Keyboard.SendKeys(&quot;%n&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;0.wma&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%P&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;P&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        '' My.Computer.Keyboard.SendKeys(&quot;^P&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;006591737839&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
    End Sub

    Private Sub TextBox2_TextChanged(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles TextBox2.TextChanged
        ' txtDataReceived.Text = TextBox2.Text
    End Sub

    Private Sub Button20_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button20.Click
        Dim c As Integer
        Dim d As Integer
        Dim ProcID As Integer
        'Dim c As Integer
        'Dim d As Integer
        ProcID = Shell(&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;, AppWinStyle.NormalFocus)
        ' c = &quot;0&quot;
        TextBox2.Text = &quot;0&quot;
        'Me.TopMost = True
        'ProcID = Form1.TextBox2.Text
        Form1a.TextBox1.Text = ProcID
        TextBox1.Text = Form1a.TextBox1.Text
        'MsgBox(ProcID)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ProcID = Form1a.TextBox1.Text
        ' ProcID = &quot;Windows Media Player&quot;
        'TextBox1.Text = ProcID
        ' On Error GoTo errorhandler
        c = TextBox1.Text
        'TextBox1.Text = Form1.TextBox1.Text
        TextBox2.Text = Form1a.TextBox3.Text
        AppActivate(&quot;Windows Media Player&quot;)
        txtDataReceived.AppendText(&quot;*&quot;)
        My.Computer.Keyboard.SendKeys(&quot;%S&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%FOn&quot;, True)
        'AppActivate(&quot;Open&quot;)
        My.Computer.Keyboard.SendKeys(&quot;%n&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;star.wma&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%P&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;P&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        '' My.Computer.Keyboard.SendKeys(&quot;^P&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;006591737839&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
    End Sub

    Private Sub Button21_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button21.Click
        Dim c As Integer
        Dim d As Integer
        Dim ProcID As Integer
        'Dim c As Integer
        'Dim d As Integer
        ProcID = Shell(&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;, AppWinStyle.NormalFocus)
        ' c = &quot;0&quot;
        TextBox2.Text = &quot;a&quot;
        'Me.TopMost = True
        'ProcID = Form1.TextBox2.Text
        Form1a.TextBox1.Text = ProcID
        TextBox1.Text = Form1a.TextBox1.Text
        'MsgBox(ProcID)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ProcID = Form1a.TextBox1.Text
        ' ProcID = &quot;Windows Media Player&quot;
        'TextBox1.Text = ProcID
        ' On Error GoTo errorhandler
        c = TextBox1.Text
        'TextBox1.Text = Form1.TextBox1.Text
        TextBox2.Text = Form1a.TextBox3.Text
        AppActivate(&quot;Windows Media Player&quot;)
        txtDataReceived.AppendText(&quot;#&quot;)
        My.Computer.Keyboard.SendKeys(&quot;%S&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%FOn&quot;, True)
        'AppActivate(&quot;Open&quot;)
        My.Computer.Keyboard.SendKeys(&quot;%n&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;has.wma&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;%P&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;#&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        '' My.Computer.Keyboard.SendKeys(&quot;^P&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;006591737839&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        txtDataReceived.AppendText(&quot;#&quot;)
    End Sub

    Public Sub New()

        ' This call is required by the Windows Form Designer.
        InitializeComponent()
        Me.TopMost = True
        ' Add any initialization after the InitializeComponent() call.

    End Sub

    Private Sub Button22_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button22.Click
        Dim ProcID As Integer
        Dim ProcID1 As Integer
        Dim a As Integer
        Dim c As Integer
        'Dim d1 As String
        Dim e1a As Integer
        ' Start the Calculator application, and store the process id.
        ' On Error GoTo errorhandler
        'GoTo Pause
        ''Form2.Show()
        '  If TextBox5.Text = 
        ProcID = Shell(&quot;C:\Program Files\Skype\Phone\Skype.exe&quot;, AppWinStyle.NormalFocus)
        ProcID1 = Shell(&quot;C:\Windows\System32\SoundRecorder.exe&quot;, AppWinStyle.NormalFocus)

        'MsgBox(ProcID)
        'Skype.Show()
        'Skype.TopMost = True
        'TextBox3.Text = ListBox1.SelectedItem
        'If Skype.TextBox1.Text = TextBox1.Text Then
        'Skype.Show()
        ' End If

        ' c = &quot;0&quot;
        'TextBox2.Text = &quot;0&quot;
        Me.TopMost = True
        ' ProcID = Form1.TextBox2.Text
        ' TextBox1.Text = ProcID
        'TextBox1.Text = Form1.TextBox1.Text
        'MsgBox(ProcID)
        'MsgBox(ProcID)
        'AppActivate(ProcID)

        'TextBox2.Text = ProcID1
        'TextBox1.Text = Form1.TextBox1.Text
        MsgBox(ProcID1)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' ProcID = 'Form1.TextBox1.Text
        'TextBox1.Text = ProcID
        'c = TextBox1.Text
        'TextBox1.Text = Form1.TextBox1.Text
        ' TextBox2.Text = Form1.TextBox3.Text
        'MsgBox(ProcID1)
        'AppActivate(ProcID1)
        TextBox4.Text = ProcID
        MsgBox(ProcID)
        'MsgBox(ProcID)
        AppActivate(ProcID)

        My.Computer.Keyboard.SendKeys(&quot;%a&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;l&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%a&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%l&quot;, True)
        My.Computer.Keyboard.SendKeys(Me.TextBox5.Text, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%a&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%l&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;123qweasdzxc&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;123qweasdzxc&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;006591737839&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        '   My.Computer.Keyboard.SendKeys(txtDataReceived.Text, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        'My.Computer.Keyboard.SendKeys(d, True)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;%&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;%al&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;%F&quot;, True)
        '  My.Computer.Keyboard.SendKeys(&quot;006591737839&quot;, True)
        '   My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        'Else

        '  End If
        'GoTo Pause
        ''Form2.TopMost() = True
        'ProcID = Shell(&quot;C:\Program Files\Voxox\Vovox.EXE&quot;, AppWinStyle.NormalFocus)
        '  Else
        '  Exit Sub
        '  End If

errorhandler:
        Exit Sub

    End Sub


    Private Shared aTimer As System.Timers.Timer

    Public Shared Sub Main()
        ' Normally, the timer is declared at the class level, 
        ' so that it stays in scope as long as it is needed. 
        ' If the timer is declared in a long-running method,   
        ' KeepAlive must be used to prevent the JIT compiler  
        ' from allowing aggressive garbage collection to occur  
        ' before the method ends. You can experiment with this 
        ' by commenting out the class-level declaration and  
        ' uncommenting the declaration below; then uncomment 
        ' the GC.KeepAlive(aTimer) at the end of the method. 
        'Dim aTimer As System.Timers.Timer 

        ' Create a timer with a ten second interval.
        aTimer = New System.Timers.Timer(10000)

        ' Hook up the Elapsed event for the timer. 
        '   AddHandler aTimer.Elapsed, AddressOf OnTimedEvent

        ' Set the Interval to 2 seconds (2000 milliseconds).
        aTimer.Interval = 2000
        aTimer.Enabled = True

        '   Console.WriteLine(&quot;Press the Enter key to exit the program.&quot;)
        '   Console.ReadLine()

        ' If the timer is declared in a long-running method, use 
        ' KeepAlive to prevent garbage collection from occurring 
        ' before the method ends. 
        'GC.KeepAlive(aTimer) 
    End Sub
    Sub OnTimedEvent(source As Object, e As ElapsedEventArgs)
        ' Console.WriteLine(&quot;The Elapsed event was raised at {0}&quot;, e.SignalTime)
 

    End Sub

    Private Sub TextBox3_DoubleClick(sender As Object, e As EventArgs) Handles TextBox3.DoubleClick

    End Sub
    'End Class
    Private Sub TextBox3_MouseDoubleClick(sender As Object, e As MouseEventArgs) Handles TextBox3.MouseDoubleClick
        ' TextBox3.Clear()
        Dim i, n, ProcID As Integer
        aTimer = New System.Timers.Timer(10000)
        For i = 0 To 9
            '  Dim msg = &quot;Do you want to continue?&quot;

            ' Display a simple message box.
            '  MsgBox(msg)

            ' Define a title for the message box. 
            '   Dim title = &quot;MsgBox Demonstration&quot;

            ' Add the title to the display.
            '     MsgBox(msg, , i)

            ' Now define a style for the message box. In this example, the 
            ' message box will have Yes and No buttons, the default will be 
            ' the No button, and a Critical Message icon will be present. 
            Dim style = MsgBoxStyle.YesNo Or MsgBoxStyle.DefaultButton2 Or _
                        MsgBoxStyle.Critical

            ' Display the message box and save the response, Yes or No. 
            Dim response = MsgBox(i, style, i)

            ' Take some action based on the response. 
            If response = MsgBoxResult.Yes Then
                txtDataReceived.AppendText(&quot;&quot;)
                ' MsgBox(&quot;YES, continue!!&quot;, , title)
                TextBox3.AppendText(i)
            ElseIf response = MsgBoxResult.No Then
                ' MsgBox(&quot;NO, stop!!&quot;, , title)
                TextBox3.AppendText(&quot;&quot;)
            End If

            ' Hook up the Elapsed event for the timer. 
            '   AddHandler aTimer.Elapsed, AddressOf OnTimedEvent

            ' Set the Interval to 2 seconds (2000 milliseconds).


            'For n = 1 To 1
            ' Button24.PerformClick()
            '  TextBox3.Text = i
            '  Timer2.Interval = 2000
            '  Timer2.Enabled = True
            '  Timer2.Start()

            'a:          If Timer2.ToString = &quot;0000&quot; Then
            ' Stop
            ' MsgBox(i)

            ' If Keys.I Then
            'handler:

            '  If MsgBox(i, MsgBoxStyle.YesNo, MsgBoxResult.Yes) Then
            ' If MsgBox(i, MsgBoxResult.Yes) Then



            'Else
            '  ElseIf MsgBoxResult.Yes = 6 Then
            ' TextBox3.AppendText(&quot;&quot;)

            ' End If
        Next i
        'End If
        Exit Sub
        '            Else
        '           GoTo a
        '            End If
        ' Else
        '  Exit Sub
        '   End If
        Me.TopMost = True
        Timer2.Stop()

        '  If txtDataReceived.Text = &quot;101&quot; Then

        '  Else

        '  End If
        '    Next n
        ' Next i
        '  GoTo handler
    End Sub

    Private Sub TextBox3_TextChanged(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles TextBox3.TextChanged






    End Sub

    Private Sub TextBox4_TextChanged(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles TextBox4.TextChanged

    End Sub

    Private Sub Button23_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button23.Click
        Dim ProcID As Integer
        'TextBox3.Text = ListBox1.SelectedItem
        ProcID = TextBox4.Text
        AppActivate(ProcID)
        My.Computer.Keyboard.SendKeys(&quot;%a&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;l&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%a&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%l&quot;, True)
        My.Computer.Keyboard.SendKeys(Me.TextBox5.Text, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%a&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%l&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;123qweasdzxc&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        ' TextBox5.Clear()
    End Sub

    Private Sub Button24_Click(sender As Object, e As EventArgs) Handles Button24.Click
        txtDataReceived.Clear()
        TextBox5.Clear()
        
    End Sub

    Private Sub TextBox5_MouseDoubleClick(sender As Object, e As MouseEventArgs) Handles TextBox5.MouseDoubleClick
        TextBox5.Text = txtDataReceived.Text
    End Sub

    Private Sub TextBox5_TextChanged(sender As Object, e As EventArgs) Handles TextBox5.TextChanged
        '  If txtDataReceived.Text = &quot;&#43;&quot; Then
        'Button23.PerformClick()
        '  txtDataReceived.Text = &quot;101&quot;
        '  End If
        '  TextBox5.Text = txtDataReceived.Text
        If TextBox5.Text = &quot;!P&quot; Then
            TextBox5.Clear()
        ElseIf TextBox5.Text = &quot;!#P&quot; Then
            TextBox5.Clear()
        ElseIf TextBox5.Text = &quot;P&quot; Then
            TextBox5.Clear()
        ElseIf TextBox5.Text = &quot;#&quot; Then
            TextBox5.Clear()
        ElseIf TextBox5.Text = &quot;!&quot; Then
            TextBox5.Clear()
        ElseIf TextBox5.Text = &quot;&#43;&quot; Then
            TextBox5.Clear()
        End If
        TextBox6.AppendText(TextBox5.Text)

    End Sub

    Private Sub Button25_Click(sender As Object, e As EventArgs) Handles Button25.Click
        Dim ProcID As Integer
        'TextBox3.Text = ListBox1.SelectedItem
        ProcID = TextBox4.Text
        AppActivate(ProcID)
        My.Computer.Keyboard.SendKeys(&quot;%S&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;S&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;%S&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;S&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;%{PGDN}&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;%a&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;%l&quot;, True)
        '  My.Computer.Keyboard.SendKeys(Me.TextBox5.Text, True)
        ' My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        '  My.Computer.Keyboard.SendKeys(&quot;%a&quot;, True)
        '  My.Computer.Keyboard.SendKeys(&quot;%l&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;123qweasdzxc&quot;, True)
        '  My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
    End Sub

    Private Sub Button26_Click(sender As Object, e As EventArgs) Handles Button26.Click
        Dim ProcID As Integer
        'TextBox3.Text = ListBox1.SelectedItem
        ProcID = TextBox4.Text
        AppActivate(ProcID)
        My.Computer.Keyboard.SendKeys(&quot;123qweasdzxc&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        TextBox5.Clear()
    End Sub

    Private Sub TextBox6_TextChanged(sender As Object, e As EventArgs) Handles TextBox6.TextChanged

    End Sub

    Private Sub Button27_Click(sender As Object, e As EventArgs) Handles Button27.Click
        Dim ProcID As Integer
        'TextBox3.Text = ListBox1.SelectedItem
        ProcID = TextBox4.Text
        AppActivate(ProcID)
        ProcID = TextBox4.Text
        AppActivate(ProcID)
        ' My.Computer.Keyboard.SendKeys(&quot;a&quot;, True)
        My.Computer.Keyboard.SendKeys(&quot;&#43;=&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;%a%a&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;%&#43;a&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;%a&quot;, True)

        ' My.Computer.Keyboard.SendKeys(&quot;%&#43;a&quot;, True)
        '  My.Computer.Keyboard.SendKeys(&quot;%a&quot;, True)
        ' My.Computer.Keyboard.SendKeys(&quot;a&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;a&quot;, True)
        'My.Computer.Keyboard.SendKeys(&quot;~&quot;, True)
        TextBox5.Clear()
    End Sub
End Class
'End Class</pre>
<div class="preview">
<pre class="vb"><span class="visualBasic__com">'http://msdn.microsoft.com/en-us/library/ms171728(VS.80).aspx</span>&nbsp;
<span class="visualBasic__com">'</span>&nbsp;
<span class="visualBasic__com">'&quot;Visual&nbsp;Basic&nbsp;Developer&nbsp;Center&quot;</span>&nbsp;
<span class="visualBasic__com">'http://msdn.microsoft.com/en-us/vbasic/default.aspx?pull=/library/en-us/vbcon/html/vboriintroductiontovisualbasic70forvisualbasicveterans.asp</span>&nbsp;
<span class="visualBasic__keyword">Imports</span>&nbsp;System&nbsp;
<span class="visualBasic__keyword">Imports</span>&nbsp;System.IO&nbsp;
<span class="visualBasic__keyword">Imports</span>&nbsp;System.IO.Ports&nbsp;
<span class="visualBasic__keyword">Imports</span>&nbsp;System.Timers&nbsp;
&nbsp;
<span class="visualBasic__com">'Public&nbsp;Class&nbsp;Timer1</span>&nbsp;
&nbsp;
<span class="visualBasic__keyword">Public</span>&nbsp;<span class="visualBasic__keyword">Class</span>&nbsp;Form1&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Private&nbsp;Property&nbsp;b&nbsp;As&nbsp;String</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Private&nbsp;Property&nbsp;OpenMode()&nbsp;As&nbsp;String</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Create&nbsp;a&nbsp;delegate&nbsp;function&nbsp;for&nbsp;this&nbsp;thread&nbsp;that&nbsp;will&nbsp;take</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;in&nbsp;a&nbsp;string&nbsp;and&nbsp;will&nbsp;write&nbsp;it&nbsp;to&nbsp;the&nbsp;txtDataReceived&nbsp;textbox</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Delegate</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;SetTextCallback(<span class="visualBasic__keyword">ByVal</span>&nbsp;[text]&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">String</span>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'****************************************************************************</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Function:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;private&nbsp;void&nbsp;UpdateCOMPortList()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Summary:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;This&nbsp;function&nbsp;updates&nbsp;the&nbsp;COM&nbsp;ports&nbsp;listbox.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Description:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;This&nbsp;function&nbsp;updates&nbsp;the&nbsp;COM&nbsp;ports&nbsp;listbox.&nbsp;&nbsp;This&nbsp;function&nbsp;is&nbsp;launched&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;periodically&nbsp;based&nbsp;on&nbsp;its&nbsp;Interval&nbsp;attribute&nbsp;(set&nbsp;in&nbsp;the&nbsp;form&nbsp;editor&nbsp;under</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;the&nbsp;properties&nbsp;window).</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Precondition:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;None</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Parameters:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;None</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Return&nbsp;Values</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;None</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Remarks:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;None</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'***************************************************************************</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;UpdateCOMPortList()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;s&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">String</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;i&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;foundDifference&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Boolean</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;i&nbsp;=&nbsp;<span class="visualBasic__number">0</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;foundDifference&nbsp;=&nbsp;<span class="visualBasic__keyword">False</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'If&nbsp;the&nbsp;number&nbsp;of&nbsp;COM&nbsp;ports&nbsp;is&nbsp;different&nbsp;than&nbsp;the&nbsp;last&nbsp;time&nbsp;we</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;checked,&nbsp;then&nbsp;we&nbsp;know&nbsp;that&nbsp;the&nbsp;COM&nbsp;ports&nbsp;have&nbsp;changed&nbsp;and&nbsp;we</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;don't&nbsp;need&nbsp;to&nbsp;verify&nbsp;each&nbsp;entry.</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;lstCOMPorts.Items.Count&nbsp;=&nbsp;SerialPort.GetPortNames().Length&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Search&nbsp;the&nbsp;entire&nbsp;SerialPort&nbsp;object.&nbsp;&nbsp;Look&nbsp;at&nbsp;COM&nbsp;port&nbsp;name</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;returned&nbsp;and&nbsp;see&nbsp;if&nbsp;it&nbsp;already&nbsp;exists&nbsp;in&nbsp;the&nbsp;list.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">For</span>&nbsp;<span class="visualBasic__keyword">Each</span>&nbsp;s&nbsp;<span class="visualBasic__keyword">In</span>&nbsp;SerialPort.GetPortNames()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'If&nbsp;any&nbsp;of&nbsp;the&nbsp;names&nbsp;have&nbsp;changed&nbsp;then&nbsp;we&nbsp;need&nbsp;to&nbsp;update&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;the&nbsp;list</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;lstCOMPorts.Items(i).Equals(s)&nbsp;=&nbsp;<span class="visualBasic__keyword">False</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;foundDifference&nbsp;=&nbsp;<span class="visualBasic__keyword">True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;i&nbsp;=&nbsp;i&nbsp;&#43;&nbsp;<span class="visualBasic__number">1</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Next</span>&nbsp;s&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Else</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;foundDifference&nbsp;=&nbsp;<span class="visualBasic__keyword">True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'If&nbsp;nothing&nbsp;has&nbsp;changed,&nbsp;exit&nbsp;the&nbsp;function.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;foundDifference&nbsp;=&nbsp;<span class="visualBasic__keyword">False</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Exit</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'If&nbsp;something&nbsp;has&nbsp;changed,&nbsp;then&nbsp;clear&nbsp;the&nbsp;list</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;lstCOMPorts.Items.Clear()&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Add&nbsp;all&nbsp;of&nbsp;the&nbsp;current&nbsp;COM&nbsp;ports&nbsp;to&nbsp;the&nbsp;list</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">For</span>&nbsp;<span class="visualBasic__keyword">Each</span>&nbsp;s&nbsp;<span class="visualBasic__keyword">In</span>&nbsp;SerialPort.GetPortNames()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;lstCOMPorts.Items.Add(s)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Next</span>&nbsp;s&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Set&nbsp;the&nbsp;listbox&nbsp;to&nbsp;point&nbsp;to&nbsp;the&nbsp;first&nbsp;entry&nbsp;in&nbsp;the&nbsp;list</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;lstCOMPorts.SelectedIndex&nbsp;=&nbsp;<span class="visualBasic__number">0</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'****************************************************************************</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Function:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;private&nbsp;void&nbsp;timer1_Tick(object&nbsp;sender,&nbsp;EventArgs&nbsp;e)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Summary:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;This&nbsp;function&nbsp;updates&nbsp;the&nbsp;COM&nbsp;ports&nbsp;listbox.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Description:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;This&nbsp;function&nbsp;updates&nbsp;the&nbsp;COM&nbsp;ports&nbsp;listbox.&nbsp;&nbsp;This&nbsp;function&nbsp;is&nbsp;launched&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;periodically&nbsp;based&nbsp;on&nbsp;its&nbsp;Interval&nbsp;attribute&nbsp;(set&nbsp;in&nbsp;the&nbsp;form&nbsp;editor&nbsp;under</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;the&nbsp;properties&nbsp;window).</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Precondition:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;None</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Parameters:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;object&nbsp;sender&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;Sender&nbsp;of&nbsp;the&nbsp;event&nbsp;(this&nbsp;form)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;EventArgs&nbsp;e&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;The&nbsp;event&nbsp;arguments</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Return&nbsp;Values</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;None</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Remarks:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;None</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'***************************************************************************/</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Timer1_Tick(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;Timer1.Tick&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Update&nbsp;the&nbsp;COM&nbsp;ports&nbsp;list&nbsp;so&nbsp;that&nbsp;we&nbsp;can&nbsp;detect</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;new&nbsp;COM&nbsp;ports&nbsp;that&nbsp;have&nbsp;been&nbsp;added.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;UpdateCOMPortList()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'****************************************************************************</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Function:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;private&nbsp;void&nbsp;btnConnect_Click(object&nbsp;sender,&nbsp;EventArgs&nbsp;e)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Summary:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;This&nbsp;function&nbsp;opens&nbsp;the&nbsp;COM&nbsp;port.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Description:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;This&nbsp;function&nbsp;opens&nbsp;the&nbsp;COM&nbsp;port.&nbsp;&nbsp;This&nbsp;function&nbsp;is&nbsp;launched&nbsp;when&nbsp;the&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;btnConnect&nbsp;button&nbsp;is&nbsp;clicked.&nbsp;&nbsp;In&nbsp;addition&nbsp;to&nbsp;opening&nbsp;the&nbsp;COM&nbsp;port,&nbsp;this&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;function&nbsp;will&nbsp;also&nbsp;change&nbsp;the&nbsp;Enable&nbsp;attribute&nbsp;of&nbsp;several&nbsp;of&nbsp;the&nbsp;form</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;objects&nbsp;to&nbsp;disable&nbsp;the&nbsp;user&nbsp;from&nbsp;opening&nbsp;a&nbsp;new&nbsp;COM&nbsp;port.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Precondition:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;None</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Parameters:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;object&nbsp;sender&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;Sender&nbsp;of&nbsp;the&nbsp;event&nbsp;(this&nbsp;form)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;EventArgs&nbsp;e&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;The&nbsp;event&nbsp;arguments</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Return&nbsp;Values</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;None</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Remarks:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;None</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'***************************************************************************/</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;btnConnect_Click(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;btnConnect.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'This&nbsp;section&nbsp;of&nbsp;code&nbsp;will&nbsp;try&nbsp;to&nbsp;open&nbsp;the&nbsp;COM&nbsp;port.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;Please&nbsp;note&nbsp;that&nbsp;it&nbsp;is&nbsp;important&nbsp;to&nbsp;use&nbsp;a&nbsp;try/catch</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;statement&nbsp;when&nbsp;opening&nbsp;the&nbsp;COM&nbsp;port.&nbsp;&nbsp;If&nbsp;a&nbsp;USB&nbsp;virtual</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;COM&nbsp;port&nbsp;is&nbsp;removed&nbsp;and&nbsp;the&nbsp;PC&nbsp;software&nbsp;tries&nbsp;to&nbsp;open</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;the&nbsp;COM&nbsp;port&nbsp;before&nbsp;it&nbsp;detects&nbsp;its&nbsp;removal&nbsp;then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;an&nbsp;exeception&nbsp;is&nbsp;thrown.&nbsp;&nbsp;If&nbsp;the&nbsp;execption&nbsp;is&nbsp;not&nbsp;in&nbsp;a</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;try/catch&nbsp;statement&nbsp;this&nbsp;could&nbsp;result&nbsp;in&nbsp;the&nbsp;application</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;crashing.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Try</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Get&nbsp;the&nbsp;port&nbsp;name&nbsp;from&nbsp;the&nbsp;application&nbsp;list&nbsp;box.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;the&nbsp;PortName&nbsp;attribute&nbsp;is&nbsp;a&nbsp;string&nbsp;name&nbsp;of&nbsp;the&nbsp;COM</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;port&nbsp;(e.g.&nbsp;-&nbsp;&quot;COM1&quot;).</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SerialPort1.PortName&nbsp;=&nbsp;lstCOMPorts.Items(lstCOMPorts.SelectedIndex).ToString()&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Open&nbsp;the&nbsp;COM&nbsp;port.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SerialPort1.Open()&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Change&nbsp;the&nbsp;state&nbsp;of&nbsp;the&nbsp;application&nbsp;objects</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;btnConnect.Enabled&nbsp;=&nbsp;<span class="visualBasic__keyword">False</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;lstCOMPorts.Enabled&nbsp;=&nbsp;<span class="visualBasic__keyword">False</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;btnClose.Enabled&nbsp;=&nbsp;<span class="visualBasic__keyword">True</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Clear&nbsp;the&nbsp;textbox&nbsp;and&nbsp;print&nbsp;that&nbsp;we&nbsp;are&nbsp;connected.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(<span class="visualBasic__string">&quot;Connected.&quot;</span>&nbsp;&#43;&nbsp;vbCrLf)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Catch</span>&nbsp;ex&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;Exception&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'If&nbsp;there&nbsp;was&nbsp;an&nbsp;exception,&nbsp;then&nbsp;close&nbsp;the&nbsp;handle&nbsp;to&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;the&nbsp;device&nbsp;and&nbsp;assume&nbsp;that&nbsp;the&nbsp;device&nbsp;was&nbsp;removed</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;btnClose_Click(<span class="visualBasic__keyword">Me</span>,&nbsp;e)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Try</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'****************************************************************************</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Function:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;private&nbsp;void&nbsp;btnClose_Click(object&nbsp;sender,&nbsp;EventArgs&nbsp;e)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Summary:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;This&nbsp;function&nbsp;closes&nbsp;the&nbsp;COM&nbsp;port.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Description:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;This&nbsp;function&nbsp;closes&nbsp;the&nbsp;COM&nbsp;port.&nbsp;&nbsp;This&nbsp;function&nbsp;is&nbsp;launched&nbsp;when&nbsp;the&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;btnClose&nbsp;button&nbsp;is&nbsp;clicked.&nbsp;&nbsp;This&nbsp;function&nbsp;can&nbsp;also&nbsp;be&nbsp;called&nbsp;directly</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;from&nbsp;other&nbsp;functions.&nbsp;&nbsp;In&nbsp;addition&nbsp;to&nbsp;closing&nbsp;the&nbsp;COM&nbsp;port,&nbsp;this&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;function&nbsp;will&nbsp;also&nbsp;change&nbsp;the&nbsp;Enable&nbsp;attribute&nbsp;of&nbsp;several&nbsp;of&nbsp;the&nbsp;form</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;objects&nbsp;to&nbsp;enable&nbsp;the&nbsp;user&nbsp;to&nbsp;open&nbsp;a&nbsp;new&nbsp;COM&nbsp;port.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Precondition:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;None</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Parameters:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;object&nbsp;sender&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;Sender&nbsp;of&nbsp;the&nbsp;event&nbsp;(this&nbsp;form)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;EventArgs&nbsp;e&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;The&nbsp;event&nbsp;arguments</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Return&nbsp;Values</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;None</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Remarks:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;None</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'***************************************************************************/</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;btnClose_Click(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;btnClose.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Reset&nbsp;the&nbsp;state&nbsp;of&nbsp;the&nbsp;application&nbsp;objects</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;btnClose.Enabled&nbsp;=&nbsp;<span class="visualBasic__keyword">False</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;btnConnect.Enabled&nbsp;=&nbsp;<span class="visualBasic__keyword">True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;lstCOMPorts.Enabled&nbsp;=&nbsp;<span class="visualBasic__keyword">True</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'This&nbsp;section&nbsp;of&nbsp;code&nbsp;will&nbsp;try&nbsp;to&nbsp;close&nbsp;the&nbsp;COM&nbsp;port.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;Please&nbsp;note&nbsp;that&nbsp;it&nbsp;is&nbsp;important&nbsp;to&nbsp;use&nbsp;a&nbsp;try/catch</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;statement&nbsp;when&nbsp;closing&nbsp;the&nbsp;COM&nbsp;port.&nbsp;&nbsp;If&nbsp;a&nbsp;USB&nbsp;virtual</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;COM&nbsp;port&nbsp;is&nbsp;removed&nbsp;and&nbsp;the&nbsp;PC&nbsp;software&nbsp;tries&nbsp;to&nbsp;close</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;the&nbsp;COM&nbsp;port&nbsp;before&nbsp;it&nbsp;detects&nbsp;its&nbsp;removal&nbsp;then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;an&nbsp;exeception&nbsp;is&nbsp;thrown.&nbsp;&nbsp;If&nbsp;the&nbsp;execption&nbsp;is&nbsp;not&nbsp;in&nbsp;a</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;try/catch&nbsp;statement&nbsp;this&nbsp;could&nbsp;result&nbsp;in&nbsp;the&nbsp;application</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;crashing.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Try</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dispose&nbsp;the&nbsp;In&nbsp;and&nbsp;Out&nbsp;buffers;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SerialPort1.DiscardInBuffer()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SerialPort1.DiscardOutBuffer()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Close&nbsp;the&nbsp;COM&nbsp;port</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SerialPort1.Close()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'If&nbsp;there&nbsp;was&nbsp;an&nbsp;exeception&nbsp;then&nbsp;there&nbsp;isn't&nbsp;much&nbsp;we&nbsp;can</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;do.&nbsp;&nbsp;The&nbsp;port&nbsp;is&nbsp;no&nbsp;longer&nbsp;available.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Catch</span>&nbsp;ex&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;Exception&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Try</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'****************************************************************************</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Function:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;private&nbsp;void&nbsp;serialPort1_DataReceived(&nbsp;&nbsp;object&nbsp;sender,&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SerialDataReceivedEventArgs&nbsp;e)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Summary:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;This&nbsp;function&nbsp;prints&nbsp;any&nbsp;data&nbsp;received&nbsp;on&nbsp;the&nbsp;COM&nbsp;port.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Description:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;This&nbsp;function&nbsp;is&nbsp;called&nbsp;when&nbsp;the&nbsp;data&nbsp;is&nbsp;received&nbsp;on&nbsp;the&nbsp;COM&nbsp;port.&nbsp;&nbsp;This</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;function&nbsp;attempts&nbsp;to&nbsp;write&nbsp;that&nbsp;data&nbsp;to&nbsp;the&nbsp;txtDataReceived&nbsp;textbox.&nbsp;&nbsp;If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;an&nbsp;exception&nbsp;occurs&nbsp;the&nbsp;btnClose_Click()&nbsp;function&nbsp;is&nbsp;called&nbsp;in&nbsp;order&nbsp;to</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;close&nbsp;the&nbsp;COM&nbsp;port&nbsp;that&nbsp;caused&nbsp;the&nbsp;exception.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Precondition:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;None</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Parameters:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;object&nbsp;sender&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;Sender&nbsp;of&nbsp;the&nbsp;event&nbsp;(this&nbsp;form)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SerialDataReceivedEventArgs&nbsp;e&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;The&nbsp;event&nbsp;arguments</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Return&nbsp;Values</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;None</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Remarks:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;None</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'***************************************************************************/</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;SerialPort1_DataReceived(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.IO.Ports.SerialDataReceivedEventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;SerialPort1.DataReceived&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'The&nbsp;ReadExisting()&nbsp;function&nbsp;will&nbsp;read&nbsp;all&nbsp;of&nbsp;the&nbsp;data&nbsp;that</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;is&nbsp;currently&nbsp;available&nbsp;in&nbsp;the&nbsp;COM&nbsp;port&nbsp;buffer.&nbsp;&nbsp;In&nbsp;this&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;example&nbsp;we&nbsp;are&nbsp;sending&nbsp;all&nbsp;of&nbsp;the&nbsp;available&nbsp;COM&nbsp;port&nbsp;data</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;to&nbsp;the&nbsp;SetText()&nbsp;function.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;NOTE:&nbsp;the&nbsp;&lt;SerialPort&gt;_DataReceived()&nbsp;function&nbsp;is&nbsp;launched</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;in&nbsp;a&nbsp;seperate&nbsp;thread&nbsp;from&nbsp;the&nbsp;rest&nbsp;of&nbsp;the&nbsp;application.&nbsp;&nbsp;A</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;delegate&nbsp;function&nbsp;is&nbsp;required&nbsp;in&nbsp;order&nbsp;to&nbsp;properly&nbsp;access</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;any&nbsp;managed&nbsp;objects&nbsp;inside&nbsp;of&nbsp;the&nbsp;other&nbsp;thread.&nbsp;&nbsp;Since&nbsp;we</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;will&nbsp;be&nbsp;writing&nbsp;to&nbsp;a&nbsp;textBox&nbsp;(a&nbsp;managed&nbsp;object)&nbsp;the&nbsp;delegate</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;function&nbsp;is&nbsp;required.&nbsp;&nbsp;Please&nbsp;see&nbsp;the&nbsp;SetText()&nbsp;function&nbsp;for&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;more&nbsp;information&nbsp;about&nbsp;delegate&nbsp;functions&nbsp;and&nbsp;how&nbsp;to&nbsp;use&nbsp;them.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Try</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SetText(SerialPort1.ReadExisting())&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Catch</span>&nbsp;ex&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;Exception&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'If&nbsp;there&nbsp;was&nbsp;an&nbsp;exception,&nbsp;then&nbsp;close&nbsp;the&nbsp;handle&nbsp;to&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;the&nbsp;device&nbsp;and&nbsp;assume&nbsp;that&nbsp;the&nbsp;device&nbsp;was&nbsp;removed</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;btnClose_Click(<span class="visualBasic__keyword">Me</span>,&nbsp;e)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Try</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'****************************************************************************</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Function:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;private&nbsp;void&nbsp;SetText(string&nbsp;text)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Summary:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;This&nbsp;function&nbsp;prints&nbsp;the&nbsp;input&nbsp;text&nbsp;to&nbsp;the&nbsp;txtDataReceived&nbsp;textbox.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Description:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;This&nbsp;function&nbsp;prints&nbsp;the&nbsp;input&nbsp;text&nbsp;to&nbsp;the&nbsp;txtDataReceived&nbsp;textbox.&nbsp;&nbsp;If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;the&nbsp;calling&nbsp;thread&nbsp;is&nbsp;the&nbsp;same&nbsp;as&nbsp;the&nbsp;thread&nbsp;that&nbsp;owns&nbsp;the&nbsp;textbox,&nbsp;then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;the&nbsp;AppendText()&nbsp;method&nbsp;is&nbsp;called&nbsp;directly.&nbsp;&nbsp;If&nbsp;a&nbsp;thread&nbsp;other&nbsp;than&nbsp;the</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;main&nbsp;thread&nbsp;calls&nbsp;this&nbsp;function,&nbsp;then&nbsp;an&nbsp;instance&nbsp;of&nbsp;the&nbsp;delegate&nbsp;function</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;is&nbsp;created&nbsp;so&nbsp;that&nbsp;the&nbsp;function&nbsp;runs&nbsp;again&nbsp;in&nbsp;the&nbsp;main&nbsp;thread.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Precondition:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;None</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Parameters:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;string&nbsp;text&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;Text&nbsp;that&nbsp;needs&nbsp;to&nbsp;be&nbsp;printed&nbsp;to&nbsp;the&nbsp;textbox</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Return&nbsp;Values</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;None</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Remarks:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;None</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'***************************************************************************/</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;SetText(<span class="visualBasic__keyword">ByVal</span>&nbsp;[text]&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">String</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'InvokeRequired&nbsp;required&nbsp;compares&nbsp;the&nbsp;thread&nbsp;ID&nbsp;of&nbsp;the</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;calling&nbsp;thread&nbsp;to&nbsp;the&nbsp;thread&nbsp;ID&nbsp;of&nbsp;the&nbsp;creating&nbsp;thread.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;If&nbsp;these&nbsp;threads&nbsp;are&nbsp;different,&nbsp;it&nbsp;returns&nbsp;true.&nbsp;&nbsp;We&nbsp;can</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;use&nbsp;this&nbsp;attribute&nbsp;to&nbsp;determine&nbsp;if&nbsp;we&nbsp;can&nbsp;append&nbsp;text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;directly&nbsp;to&nbsp;the&nbsp;textbox&nbsp;or&nbsp;if&nbsp;we&nbsp;must&nbsp;launch&nbsp;an&nbsp;a&nbsp;delegate</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;function&nbsp;instance&nbsp;to&nbsp;write&nbsp;to&nbsp;the&nbsp;textbox.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;txtDataReceived.InvokeRequired&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'InvokeRequired&nbsp;returned&nbsp;TRUE&nbsp;meaning&nbsp;that&nbsp;this&nbsp;function</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;was&nbsp;called&nbsp;from&nbsp;a&nbsp;thread&nbsp;different&nbsp;than&nbsp;the&nbsp;current</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;thread.&nbsp;&nbsp;We&nbsp;must&nbsp;launch&nbsp;a&nbsp;deleage&nbsp;function.</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Create&nbsp;an&nbsp;instance&nbsp;of&nbsp;the&nbsp;SetTextCallback&nbsp;delegate&nbsp;and</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;assign&nbsp;the&nbsp;delegate&nbsp;function&nbsp;to&nbsp;be&nbsp;this&nbsp;function.&nbsp;&nbsp;This</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;effectively&nbsp;causes&nbsp;this&nbsp;same&nbsp;SetText()&nbsp;function&nbsp;to&nbsp;be</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;called&nbsp;within&nbsp;the&nbsp;main&nbsp;thread&nbsp;instead&nbsp;of&nbsp;the&nbsp;second</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;thread.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;d&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">New</span>&nbsp;SetTextCallback(<span class="visualBasic__keyword">AddressOf</span>&nbsp;SetText)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Invoke&nbsp;the&nbsp;new&nbsp;delegate&nbsp;sending&nbsp;the&nbsp;same&nbsp;text&nbsp;to&nbsp;the</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;delegate&nbsp;that&nbsp;was&nbsp;passed&nbsp;into&nbsp;this&nbsp;function&nbsp;from&nbsp;the</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;other&nbsp;thread.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Invoke(d,&nbsp;<span class="visualBasic__keyword">New</span>&nbsp;<span class="visualBasic__keyword">Object</span>()&nbsp;{[text]})&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Else</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'If&nbsp;this&nbsp;function&nbsp;was&nbsp;called&nbsp;from&nbsp;the&nbsp;same&nbsp;thread&nbsp;that&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;holds&nbsp;the&nbsp;required&nbsp;objects&nbsp;then&nbsp;just&nbsp;add&nbsp;the&nbsp;text.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Text&nbsp;=&nbsp;(text)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.AppendText(text)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceivedd.AppendText((text))&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'****************************************************************************</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Function:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;private&nbsp;void&nbsp;btnSendData_Click(object&nbsp;sender,&nbsp;EventArgs&nbsp;e)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Summary:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;This&nbsp;function&nbsp;will&nbsp;attempt&nbsp;to&nbsp;send&nbsp;the&nbsp;contents&nbsp;of&nbsp;txtData&nbsp;over&nbsp;the&nbsp;COM&nbsp;port</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Description:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;This&nbsp;function&nbsp;is&nbsp;called&nbsp;when&nbsp;the&nbsp;btnSendData&nbsp;button&nbsp;is&nbsp;clicked.&nbsp;&nbsp;It&nbsp;will&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;attempt&nbsp;to&nbsp;send&nbsp;the&nbsp;contents&nbsp;of&nbsp;txtData&nbsp;over&nbsp;the&nbsp;COM&nbsp;port.&nbsp;&nbsp;If&nbsp;the&nbsp;attempt</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;is&nbsp;unsuccessful&nbsp;this&nbsp;function&nbsp;will&nbsp;call&nbsp;the&nbsp;btnClose_Click()&nbsp;in&nbsp;order&nbsp;to</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;close&nbsp;the&nbsp;COM&nbsp;port&nbsp;that&nbsp;just&nbsp;failed.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Precondition:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;None</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Parameters:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;object&nbsp;sender&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;Sender&nbsp;of&nbsp;the&nbsp;event&nbsp;(this&nbsp;form)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;EventArgs&nbsp;e&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;The&nbsp;event&nbsp;arguments</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Return&nbsp;Values</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;None</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Remarks:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;None</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'***************************************************************************/</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;btnSendData_Click(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;btnSendData.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'This&nbsp;section&nbsp;of&nbsp;code&nbsp;will&nbsp;try&nbsp;to&nbsp;write&nbsp;to&nbsp;the&nbsp;COM&nbsp;port.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;Please&nbsp;note&nbsp;that&nbsp;it&nbsp;is&nbsp;important&nbsp;to&nbsp;use&nbsp;a&nbsp;try/catch</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;statement&nbsp;when&nbsp;writing&nbsp;to&nbsp;the&nbsp;COM&nbsp;port.&nbsp;&nbsp;If&nbsp;a&nbsp;USB&nbsp;virtual</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;COM&nbsp;port&nbsp;is&nbsp;removed&nbsp;and&nbsp;the&nbsp;PC&nbsp;software&nbsp;tries&nbsp;to&nbsp;write</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;to&nbsp;the&nbsp;COM&nbsp;port&nbsp;before&nbsp;it&nbsp;detects&nbsp;its&nbsp;removal&nbsp;then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;an&nbsp;exeception&nbsp;is&nbsp;thrown.&nbsp;&nbsp;If&nbsp;the&nbsp;execption&nbsp;is&nbsp;not&nbsp;in&nbsp;a</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;try/catch&nbsp;statement&nbsp;this&nbsp;could&nbsp;result&nbsp;in&nbsp;the&nbsp;application</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;crashing.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Try</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Write&nbsp;the&nbsp;data&nbsp;in&nbsp;the&nbsp;text&nbsp;box&nbsp;to&nbsp;the&nbsp;open&nbsp;serial&nbsp;port</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtData.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;12&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SerialPort1.Write(txtData.Text)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Button23.PerformClick()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Catch</span>&nbsp;ex&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;Exception&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'If&nbsp;there&nbsp;was&nbsp;an&nbsp;exception,&nbsp;then&nbsp;close&nbsp;the&nbsp;handle&nbsp;to&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;the&nbsp;device&nbsp;and&nbsp;assume&nbsp;that&nbsp;the&nbsp;device&nbsp;was&nbsp;removed</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;btnClose_Click(<span class="visualBasic__keyword">Me</span>,&nbsp;e)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Try</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;txtDataReceived_MouseClick(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.Windows.Forms.MouseEventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;txtDataReceived.MouseClick&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;txtDataReceived_MouseDoubleClick(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.Windows.Forms.MouseEventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;txtDataReceived.MouseDoubleClick&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Test1()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">On</span>&nbsp;<span class="visualBasic__keyword">Error</span>&nbsp;<span class="visualBasic__keyword">Resume</span>&nbsp;<span class="visualBasic__keyword">Next</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;text&nbsp;As&nbsp;String</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Me</span>.TopMost&nbsp;=&nbsp;<span class="visualBasic__keyword">True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;txtDataReceived.Clear()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;i,&nbsp;n&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;aTimer&nbsp;=&nbsp;<span class="visualBasic__keyword">New</span>&nbsp;System.Timers.Timer(<span class="visualBasic__number">10000</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Me</span>.TopMost&nbsp;=&nbsp;<span class="visualBasic__keyword">True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">For</span>&nbsp;i&nbsp;=&nbsp;<span class="visualBasic__number">1</span>&nbsp;<span class="visualBasic__keyword">To</span>&nbsp;<span class="visualBasic__number">10</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;msg&nbsp;=&nbsp;<span class="visualBasic__string">&quot;Do&nbsp;you&nbsp;want&nbsp;to&nbsp;continue?&quot;</span>&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Display&nbsp;a&nbsp;simple&nbsp;message&nbsp;box.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MsgBox(msg)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Define&nbsp;a&nbsp;title&nbsp;for&nbsp;the&nbsp;message&nbsp;box.&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;title&nbsp;=&nbsp;<span class="visualBasic__string">&quot;MsgBox&nbsp;Demonstration&quot;</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Add&nbsp;the&nbsp;title&nbsp;to&nbsp;the&nbsp;display.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MsgBox(msg,&nbsp;,&nbsp;i)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Now&nbsp;define&nbsp;a&nbsp;style&nbsp;for&nbsp;the&nbsp;message&nbsp;box.&nbsp;In&nbsp;this&nbsp;example,&nbsp;the&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;message&nbsp;box&nbsp;will&nbsp;have&nbsp;Yes&nbsp;and&nbsp;No&nbsp;buttons,&nbsp;the&nbsp;default&nbsp;will&nbsp;be&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;the&nbsp;No&nbsp;button,&nbsp;and&nbsp;a&nbsp;Critical&nbsp;Message&nbsp;icon&nbsp;will&nbsp;be&nbsp;present.&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;style&nbsp;=&nbsp;MsgBoxStyle.YesNo&nbsp;<span class="visualBasic__keyword">Or</span>&nbsp;MsgBoxStyle.DefaultButton2&nbsp;<span class="visualBasic__keyword">Or</span>&nbsp;_&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MsgBoxStyle.Critical&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Display&nbsp;the&nbsp;message&nbsp;box&nbsp;and&nbsp;save&nbsp;the&nbsp;response,&nbsp;Yes&nbsp;or&nbsp;No.&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;response&nbsp;=&nbsp;MsgBox(msg,&nbsp;style,&nbsp;title)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Take&nbsp;some&nbsp;action&nbsp;based&nbsp;on&nbsp;the&nbsp;response.&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;response&nbsp;=&nbsp;MsgBoxResult.Yes&nbsp;&amp;&nbsp;TextBox5.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;101&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MsgBox(<span class="visualBasic__string">&quot;YES,&nbsp;continue!!&quot;</span>,&nbsp;,&nbsp;title)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox3.AppendText(i)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Exit&nbsp;Sub</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;txtDataReceived.Clear()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Else</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MsgBox(<span class="visualBasic__string">&quot;NO,&nbsp;stop!!&quot;</span>,&nbsp;,&nbsp;title)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox3.AppendText(<span class="visualBasic__string">&quot;&quot;</span>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Exit&nbsp;Sub</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Hook&nbsp;up&nbsp;the&nbsp;Elapsed&nbsp;event&nbsp;for&nbsp;the&nbsp;timer.&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;AddHandler&nbsp;aTimer.Elapsed,&nbsp;AddressOf&nbsp;OnTimedEvent</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Set&nbsp;the&nbsp;Interval&nbsp;to&nbsp;2&nbsp;seconds&nbsp;(2000&nbsp;milliseconds).</span>&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'For&nbsp;n&nbsp;=&nbsp;1&nbsp;To&nbsp;1</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Button24.PerformClick()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;TextBox3.Text&nbsp;=&nbsp;i</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;Timer2.Interval&nbsp;=&nbsp;2000</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;Timer2.Enabled&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;Timer2.Start()</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'a:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;If&nbsp;Timer2.ToString&nbsp;=&nbsp;&quot;0000&quot;&nbsp;Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Stop</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;MsgBox(i)</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;If&nbsp;Keys.I&nbsp;Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'handler:</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;If&nbsp;MsgBox(i,&nbsp;MsgBoxStyle.YesNo,&nbsp;MsgBoxResult.Yes)&nbsp;Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;If&nbsp;MsgBox(i,&nbsp;MsgBoxResult.Yes)&nbsp;Then</span>&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Else</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;ElseIf&nbsp;MsgBoxResult.Yes&nbsp;=&nbsp;6&nbsp;Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;TextBox3.AppendText(&quot;&quot;)</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;End&nbsp;If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Next</span>&nbsp;i&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'End&nbsp;If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Exit</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;txtDataReceived_TextChanged(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;txtDataReceived.TextChanged&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Dim&nbsp;a&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;a&nbsp;=&nbsp;2</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">For</span>&nbsp;a&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;=&nbsp;<span class="visualBasic__number">1</span>&nbsp;<span class="visualBasic__keyword">To</span>&nbsp;<span class="visualBasic__number">2</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;If&nbsp;txtDataReceived.Text&nbsp;=&nbsp;&quot;1&quot;&nbsp;Or&nbsp;&quot;2&quot;&nbsp;Or&nbsp;&quot;3&quot;&nbsp;Or&nbsp;&quot;4&quot;&nbsp;Or&nbsp;&quot;5&quot;&nbsp;Or&nbsp;&quot;6&quot;&nbsp;Or&nbsp;&quot;7&quot;&nbsp;Or&nbsp;&quot;8&quot;&nbsp;Or&nbsp;&quot;9&quot;&nbsp;Or&nbsp;&quot;0&quot;&nbsp;Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;I&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'For&nbsp;I&nbsp;=&nbsp;1&nbsp;To&nbsp;1000&nbsp;&nbsp;'&nbsp;Loop&nbsp;100&nbsp;times.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Beep()&nbsp;&nbsp;&nbsp;'&nbsp;Sound&nbsp;a&nbsp;tone.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Next&nbsp;I</span>&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;&#43;&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;txtDataReceived.AppendText(&quot;0&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;MsgBox(&quot;&#43;&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button23.PerformClick()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;ElseIf&nbsp;txtDataReceived.Text&nbsp;=&nbsp;&quot;&#43;&quot;&nbsp;Then&nbsp;'And&nbsp;txtDataReceived.Text&nbsp;=&nbsp;&quot;&#43;&quot;&nbsp;Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button27.PerformClick()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;Button24.PerformClick()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ElseIf&nbsp;txtDataReceived.Text&nbsp;=&nbsp;&quot;!P&quot;&nbsp;Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;#&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;txtDataReceived.AppendText(&quot;1&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button26.PerformClick()&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;btnSendData.PerformClick()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;btnSendData.PerformClick()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;btnSendData.PerformClick()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;btnSendData.PerformClick()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;btnSendData.PerformClick()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;btnSendData.PerformClick()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;btnSendData.PerformClick()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;btnSendData.PerformClick()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button25.PerformClick()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;A&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;A&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.AppendText(<span class="visualBasic__string">&quot;AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;txtDataReceived.AppendText(&quot;2&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Button11.PerformClick()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;b&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;B&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.AppendText(<span class="visualBasic__string">&quot;BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;txtDataReceived.AppendText(&quot;2&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Button11.PerformClick()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;2&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;2&quot;</span>&nbsp;<span class="visualBasic__com">'Hex(38)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;a&nbsp;=&nbsp;Keys.Up&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.AppendText(<span class="visualBasic__string">&quot;2222222222222222222222222222222222222222222222222222222222&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;If&nbsp;txtDataReceived.Text&nbsp;=&nbsp;Hex(38)&nbsp;Then&nbsp;TextBox5.Text&nbsp;=&nbsp;Hex(38)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;txtDataReceived.AppendText(&quot;2&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Button11.PerformClick()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;8&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;8&quot;</span>&nbsp;<span class="visualBasic__com">'Keys.Down</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.AppendText(<span class="visualBasic__string">&quot;888888888888888888888888888888888888888888888888888888888888888&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'If&nbsp;TextBox5.Text&nbsp;=&nbsp;&quot;8&quot;&nbsp;Then&nbsp;TextBox5.Text&nbsp;=&nbsp;Keys.Down</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;4&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;4&quot;</span>&nbsp;<span class="visualBasic__com">'Keys.Left</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.AppendText(<span class="visualBasic__string">&quot;4444444444444444444444444444444444444444444444444444444444444444&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'If&nbsp;TextBox5.Text&nbsp;=&nbsp;&quot;4&quot;&nbsp;Then&nbsp;TextBox5.Text&nbsp;=&nbsp;Keys.Left</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;txtDataReceived.AppendText(&quot;2&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Button11.PerformClick()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;6&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;6&quot;</span>&nbsp;<span class="visualBasic__com">'Keys.Right</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.AppendText(<span class="visualBasic__string">&quot;666666666666666666666666666666666666666666666666666666666666666666666&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'If&nbsp;TextBox5.Text&nbsp;=&nbsp;&quot;6&quot;&nbsp;Then&nbsp;TextBox5.Text&nbsp;=&nbsp;Keys.Right</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;s&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;txtDataReceived.AppendText(&quot;2&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button11.PerformClick()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;t&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(&quot;3&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button12.PerformClick()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;u&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(&quot;4&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button13.PerformClick()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;v&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(&quot;5&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button14.PerformClick()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;w&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(&quot;6&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button15.PerformClick()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;x&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(&quot;7&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button16.PerformClick()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;y&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(&quot;8&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button17.PerformClick()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;p&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(&quot;9&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button18.PerformClick()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ElseIf&nbsp;Keys.NumPad6&nbsp;Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Text&nbsp;=&nbsp;&quot;6&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;TextBox5.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;P&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;Else&nbsp;:&nbsp;TextBox5.Clear()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;TextBox5.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;#&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;TextBox5.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;!&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;TextBox5.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;!#P&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;TextBox5.Clear()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Next</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Else</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;GoTo&nbsp;a</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;End&nbsp;If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Else</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;Exit&nbsp;Sub</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;End&nbsp;If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Me.TopMost&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;Timer2.Stop()</span>&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Button24.PerformClick()</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;test()&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;1&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button10.<span class="visualBasic__keyword">Select</span>()&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;d&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;c&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;d&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Shell(<span class="visualBasic__string">&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;</span>,&nbsp;AppWinStyle.NormalFocus)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;c&nbsp;=&nbsp;&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Forms.Form1.Button10.&nbsp;&nbsp;&nbsp;&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Me.TopMost&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ProcID&nbsp;=&nbsp;Form1.TextBox2.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Form1a.TextBox1.Text&nbsp;=&nbsp;ProcID&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox1.Text&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;ProcID&nbsp;=&nbsp;&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;ProcID</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;On&nbsp;Error&nbsp;GoTo&nbsp;errorhandler</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c&nbsp;=&nbsp;TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;Form1a.TextBox3.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(<span class="visualBasic__string">&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%S&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%FOn&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'AppActivate(&quot;Open&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%n&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;1.wma&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;~&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%P&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox3.AppendText(<span class="visualBasic__string">&quot;1&quot;</span>)&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;2&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button11.<span class="visualBasic__keyword">Select</span>()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;d&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;c&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;d&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Shell(<span class="visualBasic__string">&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;</span>,&nbsp;AppWinStyle.NormalFocus)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;c&nbsp;=&nbsp;&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Forms.Form1.Button10.&nbsp;&nbsp;&nbsp;&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Me.TopMost&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ProcID&nbsp;=&nbsp;Form1.TextBox2.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Form1a.TextBox1.Text&nbsp;=&nbsp;ProcID&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox1.Text&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;ProcID&nbsp;=&nbsp;&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;ProcID</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;On&nbsp;Error&nbsp;GoTo&nbsp;errorhandler</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c&nbsp;=&nbsp;TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;Form1a.TextBox3.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(<span class="visualBasic__string">&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%S&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%FOn&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'AppActivate(&quot;Open&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%n&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;2.wma&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;~&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%P&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox3.AppendText(<span class="visualBasic__string">&quot;2&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;3&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button12.<span class="visualBasic__keyword">Select</span>()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;d&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;c&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;d&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Shell(<span class="visualBasic__string">&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;</span>,&nbsp;AppWinStyle.NormalFocus)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;c&nbsp;=&nbsp;&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Forms.Form1.Button10.&nbsp;&nbsp;&nbsp;&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Me.TopMost&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ProcID&nbsp;=&nbsp;Form1.TextBox2.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Form1a.TextBox1.Text&nbsp;=&nbsp;ProcID&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox1.Text&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;ProcID&nbsp;=&nbsp;&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;ProcID</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;On&nbsp;Error&nbsp;GoTo&nbsp;errorhandler</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c&nbsp;=&nbsp;TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;Form1a.TextBox3.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(<span class="visualBasic__string">&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%S&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%FOn&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'AppActivate(&quot;Open&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%n&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;3.wma&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;~&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%P&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox3.AppendText(<span class="visualBasic__string">&quot;3&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Clear()&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;4&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button13.<span class="visualBasic__keyword">Select</span>()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;d&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;c&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;d&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Shell(<span class="visualBasic__string">&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;</span>,&nbsp;AppWinStyle.NormalFocus)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;c&nbsp;=&nbsp;&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Forms.Form1.Button10.&nbsp;&nbsp;&nbsp;&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Me.TopMost&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ProcID&nbsp;=&nbsp;Form1.TextBox2.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Form1a.TextBox1.Text&nbsp;=&nbsp;ProcID&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox1.Text&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;ProcID&nbsp;=&nbsp;&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;ProcID</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;On&nbsp;Error&nbsp;GoTo&nbsp;errorhandler</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c&nbsp;=&nbsp;TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;Form1a.TextBox3.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(<span class="visualBasic__string">&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%S&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%FOn&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'AppActivate(&quot;Open&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%n&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;4.wma&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;~&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%P&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox3.AppendText(<span class="visualBasic__string">&quot;4&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;5&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button14.<span class="visualBasic__keyword">Select</span>()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;d&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;c&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;d&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Shell(<span class="visualBasic__string">&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;</span>,&nbsp;AppWinStyle.NormalFocus)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;c&nbsp;=&nbsp;&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Forms.Form1.Button10.&nbsp;&nbsp;&nbsp;&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Me.TopMost&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ProcID&nbsp;=&nbsp;Form1.TextBox2.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Form1a.TextBox1.Text&nbsp;=&nbsp;ProcID&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox1.Text&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;ProcID&nbsp;=&nbsp;&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;ProcID</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;On&nbsp;Error&nbsp;GoTo&nbsp;errorhandler</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c&nbsp;=&nbsp;TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;Form1a.TextBox3.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(<span class="visualBasic__string">&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%S&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%FOn&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'AppActivate(&quot;Open&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%n&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;5.wma&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;~&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%P&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox3.AppendText(<span class="visualBasic__string">&quot;5&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;6&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button15.<span class="visualBasic__keyword">Select</span>()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;d&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;c&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;d&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Shell(<span class="visualBasic__string">&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;</span>,&nbsp;AppWinStyle.NormalFocus)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;c&nbsp;=&nbsp;&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Forms.Form1.Button10.&nbsp;&nbsp;&nbsp;&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Me.TopMost&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ProcID&nbsp;=&nbsp;Form1.TextBox2.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Form1a.TextBox1.Text&nbsp;=&nbsp;ProcID&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox1.Text&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;ProcID&nbsp;=&nbsp;&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;ProcID</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;On&nbsp;Error&nbsp;GoTo&nbsp;errorhandler</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c&nbsp;=&nbsp;TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;Form1a.TextBox3.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(<span class="visualBasic__string">&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%S&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%FOn&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'AppActivate(&quot;Open&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%n&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;6.wma&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;~&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%P&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox3.AppendText(<span class="visualBasic__string">&quot;6&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;7&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button16.<span class="visualBasic__keyword">Select</span>()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;d&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;c&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;d&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Shell(<span class="visualBasic__string">&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;</span>,&nbsp;AppWinStyle.NormalFocus)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;c&nbsp;=&nbsp;&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Forms.Form1.Button10.&nbsp;&nbsp;&nbsp;&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Me.TopMost&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ProcID&nbsp;=&nbsp;Form1.TextBox2.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Form1a.TextBox1.Text&nbsp;=&nbsp;ProcID&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox1.Text&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;ProcID&nbsp;=&nbsp;&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;ProcID</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;On&nbsp;Error&nbsp;GoTo&nbsp;errorhandler</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c&nbsp;=&nbsp;TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;Form1a.TextBox3.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(<span class="visualBasic__string">&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%S&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%FOn&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'AppActivate(&quot;Open&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%n&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;7.wma&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;~&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%P&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox3.AppendText(<span class="visualBasic__string">&quot;7&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;8&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button17.<span class="visualBasic__keyword">Select</span>()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;d&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;c&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;d&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Shell(<span class="visualBasic__string">&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;</span>,&nbsp;AppWinStyle.NormalFocus)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;c&nbsp;=&nbsp;&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Forms.Form1.Button10.&nbsp;&nbsp;&nbsp;&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Me.TopMost&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ProcID&nbsp;=&nbsp;Form1.TextBox2.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Form1a.TextBox1.Text&nbsp;=&nbsp;ProcID&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox1.Text&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;ProcID&nbsp;=&nbsp;&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;ProcID</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;On&nbsp;Error&nbsp;GoTo&nbsp;errorhandler</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c&nbsp;=&nbsp;TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;Form1a.TextBox3.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(<span class="visualBasic__string">&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%S&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%FOn&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'AppActivate(&quot;Open&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%n&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;8.wma&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;~&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%P&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox3.AppendText(<span class="visualBasic__string">&quot;8&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;9&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button18.<span class="visualBasic__keyword">Select</span>()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;d&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;c&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;d&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Shell(<span class="visualBasic__string">&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;</span>,&nbsp;AppWinStyle.NormalFocus)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;c&nbsp;=&nbsp;&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Forms.Form1.Button10.&nbsp;&nbsp;&nbsp;&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Me.TopMost&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ProcID&nbsp;=&nbsp;Form1.TextBox2.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Form1a.TextBox1.Text&nbsp;=&nbsp;ProcID&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox1.Text&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;ProcID&nbsp;=&nbsp;&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;ProcID</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;On&nbsp;Error&nbsp;GoTo&nbsp;errorhandler</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c&nbsp;=&nbsp;TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;Form1a.TextBox3.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(<span class="visualBasic__string">&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%S&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%FOn&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'AppActivate(&quot;Open&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%n&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;9.wma&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;~&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%P&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox3.AppendText(<span class="visualBasic__string">&quot;9&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;0&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button19.<span class="visualBasic__keyword">Select</span>()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;d&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;c&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;d&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Shell(<span class="visualBasic__string">&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;</span>,&nbsp;AppWinStyle.NormalFocus)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;c&nbsp;=&nbsp;&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Forms.Form1.Button10.&nbsp;&nbsp;&nbsp;&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Me.TopMost&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ProcID&nbsp;=&nbsp;Form1.TextBox2.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Form1a.TextBox1.Text&nbsp;=&nbsp;ProcID&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox1.Text&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;ProcID&nbsp;=&nbsp;&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;ProcID</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;On&nbsp;Error&nbsp;GoTo&nbsp;errorhandler</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c&nbsp;=&nbsp;TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;Form1a.TextBox3.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(<span class="visualBasic__string">&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%S&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%FOn&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'AppActivate(&quot;Open&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%n&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;0.wma&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;~&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%P&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox3.AppendText(<span class="visualBasic__string">&quot;0&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;b&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button20.<span class="visualBasic__keyword">Select</span>()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;d&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;c&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;d&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Shell(<span class="visualBasic__string">&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;</span>,&nbsp;AppWinStyle.NormalFocus)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;c&nbsp;=&nbsp;&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Forms.Form1.Button10.&nbsp;&nbsp;&nbsp;&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Me.TopMost&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ProcID&nbsp;=&nbsp;Form1.TextBox2.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Form1a.TextBox1.Text&nbsp;=&nbsp;ProcID&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox1.Text&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;ProcID&nbsp;=&nbsp;&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;ProcID</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;On&nbsp;Error&nbsp;GoTo&nbsp;errorhandler</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c&nbsp;=&nbsp;TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;Form1a.TextBox3.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(<span class="visualBasic__string">&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%S&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%FOn&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'AppActivate(&quot;Open&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%n&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;star.wma&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;~&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%P&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox3.AppendText(<span class="visualBasic__string">&quot;*&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;a&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button21.<span class="visualBasic__keyword">Select</span>()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;d&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;c&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;d&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Shell(<span class="visualBasic__string">&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;</span>,&nbsp;AppWinStyle.NormalFocus)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;c&nbsp;=&nbsp;&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Forms.Form1.Button10.&nbsp;&nbsp;&nbsp;&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Me.TopMost&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ProcID&nbsp;=&nbsp;Form1.TextBox2.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Form1a.TextBox1.Text&nbsp;=&nbsp;ProcID&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox1.Text&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;ProcID&nbsp;=&nbsp;&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;ProcID</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;On&nbsp;Error&nbsp;GoTo&nbsp;errorhandler</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c&nbsp;=&nbsp;TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;Form1a.TextBox3.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(<span class="visualBasic__string">&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%S&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%FOn&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'AppActivate(&quot;Open&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%n&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;has.wma&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;~&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%P&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox3.AppendText(<span class="visualBasic__string">&quot;#&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;&#43;&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;txtDataReceived.AppendText(&quot;0&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;MsgBox(&quot;&#43;&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button23.PerformClick()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;ElseIf&nbsp;txtDataReceived.Text&nbsp;=&nbsp;&quot;&#43;&quot;&nbsp;Then&nbsp;'And&nbsp;txtDataReceived.Text&nbsp;=&nbsp;&quot;&#43;&quot;&nbsp;Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button27.PerformClick()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;Button24.PerformClick()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ElseIf&nbsp;txtDataReceived.Text&nbsp;=&nbsp;&quot;!P&quot;&nbsp;Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;#&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;txtDataReceived.AppendText(&quot;1&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button26.PerformClick()&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;btnSendData.PerformClick()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;btnSendData.PerformClick()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;btnSendData.PerformClick()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;btnSendData.PerformClick()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;btnSendData.PerformClick()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;btnSendData.PerformClick()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;btnSendData.PerformClick()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;btnSendData.PerformClick()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button25.PerformClick()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;s&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;txtDataReceived.AppendText(&quot;2&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button11.PerformClick()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;t&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(&quot;3&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button12.PerformClick()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;u&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(&quot;4&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button13.PerformClick()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;v&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(&quot;5&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button14.PerformClick()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;w&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(&quot;6&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button15.PerformClick()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;x&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(&quot;7&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button16.PerformClick()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;y&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(&quot;8&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button17.PerformClick()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;txtDataReceived.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;p&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(&quot;9&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button18.PerformClick()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ElseIf&nbsp;Keys.NumPad6&nbsp;Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Text&nbsp;=&nbsp;&quot;6&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;TextBox5.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;P&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;Else&nbsp;:&nbsp;TextBox5.Clear()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;TextBox5.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;#&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;TextBox5.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;!&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;TextBox5.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;!#P&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;TextBox5.Clear()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;End&nbsp;If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;TextBox1_TextChanged(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;txtDataReceivedd.TextChanged&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;txtData_TextChanged(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;txtData.TextChanged&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox1.Text&nbsp;=&nbsp;txtData.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;TextBox1_TextChanged_1(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Button1_Click(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Object</span>,&nbsp;_&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;Button1.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;psi&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">New</span>&nbsp;&nbsp;_&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;System.Diagnostics.ProcessStartInfo(<span class="visualBasic__string">&quot;C:\windows\system32\calc.exe&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;psi.RedirectStandardOutput&nbsp;=&nbsp;<span class="visualBasic__keyword">True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;psi.WindowStyle&nbsp;=&nbsp;ProcessWindowStyle.Hidden&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;psi.UseShellExecute&nbsp;=&nbsp;<span class="visualBasic__keyword">False</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;listFiles&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.Diagnostics.Process&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;listFiles&nbsp;=&nbsp;System.Diagnostics.Process.Start(psi)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;myOutput&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.IO.StreamReader&nbsp;_&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;=&nbsp;listFiles.StandardOutput&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;listFiles.WaitForExit(<span class="visualBasic__number">2000</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;listFiles.HasExited&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;output&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">String</span>&nbsp;=&nbsp;myOutput.ReadToEnd&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Debug.WriteLine(output)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Button2_Click(sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;Button2.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;Filename&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">String</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;Res&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">String</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;sData&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;sNWind&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">String</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;a&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Byte</span>&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;a1&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'On&nbsp;Error&nbsp;Resume&nbsp;Next</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&quot;C:\Users\House\Desktop\a.txt&quot;</span>&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Res&nbsp;=&nbsp;Shell(Chr(<span class="visualBasic__number">34</span>)&nbsp;&amp;&nbsp;<span class="visualBasic__string">&quot;C:\Windows\System32\calc.exe&quot;</span>,&nbsp;vbMaximizedFocus)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Print(&quot;C:\Windows\System32\calc.exe&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Res&nbsp;=&nbsp;(a1)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Print(Shell(Chr(<span class="visualBasic__number">34</span>)&nbsp;&amp;&nbsp;<span class="visualBasic__string">&quot;C:\Users\House\Desktop\a.txt&quot;</span>&nbsp;&amp;&nbsp;Chr(<span class="visualBasic__number">34</span>)),&nbsp;a1)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Close&nbsp;the&nbsp;connection</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'rs.Close()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;conn.Close()</span>&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Filename&nbsp;=&nbsp;<span class="visualBasic__string">&quot;C:\windows\system32\calc.exe&quot;</span>&nbsp;<span class="visualBasic__com">'Check&nbsp;file&nbsp;is&nbsp;here&nbsp;first</span>&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;Dir(Filename)&nbsp;=&nbsp;<span class="visualBasic__string">&quot;&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MsgBox(Filename&nbsp;&amp;&nbsp;<span class="visualBasic__string">&quot;&nbsp;not&nbsp;found&quot;</span>,&nbsp;vbInformation)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Else</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Res&nbsp;=&nbsp;Shell(&quot;Calculator.exe&nbsp;&quot;&nbsp;&amp;&nbsp;Filename,&nbsp;vbHide)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Res&nbsp;=&nbsp;Shell(<span class="visualBasic__string">&quot;C:\Users\House\Desktop\VB.net&nbsp;2005&nbsp;Simple&nbsp;CDC&nbsp;Demo&nbsp;&quot;</span>&nbsp;&amp;&nbsp;_&nbsp;
&nbsp;&nbsp;txtData.Text,&nbsp;vbMaximizedFocus)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button3.Enabled&nbsp;=&nbsp;<span class="visualBasic__keyword">True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Button3_Click()&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Button3_Click()&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;Button3.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;Res&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">String</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Res&nbsp;=&nbsp;Shell(<span class="visualBasic__string">&quot;C:\Users\House\Desktop\VB.net&nbsp;2005&nbsp;Simple&nbsp;CDC&nbsp;Demo&nbsp;&quot;</span>&nbsp;&amp;&nbsp;_&nbsp;
&nbsp;&nbsp;txtData.Text,&nbsp;vbMaximizedFocus)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Function</span>&nbsp;KeyPressEventArgs()&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;Type&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">On</span>&nbsp;<span class="visualBasic__keyword">Error</span>&nbsp;<span class="visualBasic__keyword">Resume</span>&nbsp;<span class="visualBasic__keyword">Next</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Throw</span>&nbsp;<span class="visualBasic__keyword">New</span>&nbsp;ApplicationException&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Code&nbsp;to&nbsp;react&nbsp;to&nbsp;possible&nbsp;causes&nbsp;of&nbsp;the&nbsp;exception.</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Function</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Function</span>&nbsp;b1()&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">String</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Throw</span>&nbsp;<span class="visualBasic__keyword">New</span>&nbsp;NotImplementedException&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Function</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Button4_Click(sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;Button4.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;oExcel&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Object</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;oBook&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Object</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;oSheet&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Object</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;oCalc&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Object</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Start&nbsp;a&nbsp;new&nbsp;workbook&nbsp;in&nbsp;Excel</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'oCalc&nbsp;=&nbsp;CreateObject(&quot;C:\windows\system32\calc.exe&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;oExcel&nbsp;=&nbsp;CreateObject(<span class="visualBasic__string">&quot;Excel.Application&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;oBook&nbsp;=&nbsp;oExcel.Workbooks.Add&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Add&nbsp;data&nbsp;to&nbsp;cells&nbsp;of&nbsp;the&nbsp;first&nbsp;worksheet&nbsp;in&nbsp;the&nbsp;new&nbsp;workbook</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;oSheet&nbsp;=&nbsp;oBook.Worksheets(<span class="visualBasic__number">1</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;oSheet.Range(<span class="visualBasic__string">&quot;A1&quot;</span>).Value&nbsp;=&nbsp;<span class="visualBasic__string">&quot;Last&nbsp;Name&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;oSheet.Range(<span class="visualBasic__string">&quot;B1&quot;</span>).Value&nbsp;=&nbsp;<span class="visualBasic__string">&quot;First&nbsp;Name&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;oSheet.Range(<span class="visualBasic__string">&quot;A1:B1&quot;</span>).Font.Bold&nbsp;=&nbsp;<span class="visualBasic__keyword">True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;oSheet.Range(<span class="visualBasic__string">&quot;A2&quot;</span>).Value&nbsp;=&nbsp;<span class="visualBasic__string">&quot;Doe&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;oSheet.Range(<span class="visualBasic__string">&quot;B2&quot;</span>).Value&nbsp;=&nbsp;<span class="visualBasic__string">&quot;John&quot;</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Save&nbsp;the&nbsp;Workbook&nbsp;and&nbsp;Quit&nbsp;Excel</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;oBook.SaveAs(<span class="visualBasic__string">&quot;C:\Book1.xls&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;oExcel.Quit()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Button5_Click(sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;Button5.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Create&nbsp;a&nbsp;new&nbsp;connection&nbsp;object&nbsp;for&nbsp;Book1.xls</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox1.Text&nbsp;=&nbsp;txtData.Text&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;TextBox1_TextChanged_2(sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;TextBox1.TextChanged&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Form1_Load(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;<span class="visualBasic__keyword">MyBase</span>.Load&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;i&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Create&nbsp;a&nbsp;timer&nbsp;with&nbsp;a&nbsp;ten&nbsp;second&nbsp;interval.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;aTimer&nbsp;=&nbsp;<span class="visualBasic__keyword">New</span>&nbsp;System.Timers.Timer(<span class="visualBasic__number">10000</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;aTimer.Interval&nbsp;=&nbsp;<span class="visualBasic__number">2000</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;aTimer.Enabled&nbsp;=&nbsp;<span class="visualBasic__keyword">True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Hook&nbsp;up&nbsp;the&nbsp;Elapsed&nbsp;event&nbsp;for&nbsp;the&nbsp;timer.&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">AddHandler</span>&nbsp;aTimer.Elapsed,&nbsp;<span class="visualBasic__keyword">AddressOf</span>&nbsp;OnTimedEvent&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Set&nbsp;the&nbsp;Interval&nbsp;to&nbsp;2&nbsp;seconds&nbsp;(2000&nbsp;milliseconds).</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Console.WriteLine(&quot;Press&nbsp;the&nbsp;Enter&nbsp;key&nbsp;to&nbsp;exit&nbsp;the&nbsp;program.&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Console.ReadLine()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Button6_Click(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;Button6.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Form1a.Show()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Button7_Click(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;Button7.Click&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Button8_Click(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;Button8.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Form1a.TextBox3.Text&nbsp;=&nbsp;txtDataReceived.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Form1a.TextBox3.Text&nbsp;=&nbsp;TextBox3.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Form1a.TextBox1.Text&nbsp;=&nbsp;Skype.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Form2.TextBox2.text&nbsp;=&nbsp;txtDataReceived.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Button9_Click(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;Button9.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;a&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;d1&nbsp;As&nbsp;String</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;e1a&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Start&nbsp;the&nbsp;Calculator&nbsp;application,&nbsp;and&nbsp;store&nbsp;the&nbsp;process&nbsp;id.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;On&nbsp;Error&nbsp;GoTo&nbsp;errorhandler</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'GoTo&nbsp;Pause</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''Form2.Show()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ProcID&nbsp;=&nbsp;Shell(&quot;C:\Program&nbsp;Files\Microsoft&nbsp;Office\Office14\Excel.exe&quot;,&nbsp;AppWinStyle.NormalFocus)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Test.Main1()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;DirAppend.Main()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'List''x1.Items.Add()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''ProcID&nbsp;=&nbsp;Shell(&quot;C:\Program&nbsp;Files\Microsoft&nbsp;Office\Office14\Excel.exe&quot;,&nbsp;AppWinStyle.NormalFocus)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Skype.Show()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Skype.TopMost&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox3.Text&nbsp;=&nbsp;ListBox1.SelectedItem</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;If&nbsp;Skype.TextBox1.Text&nbsp;=&nbsp;TextBox1.Text&nbsp;Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Skype.Show()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;End&nbsp;If</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;c&nbsp;=&nbsp;&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox2.Text&nbsp;=&nbsp;&quot;0&quot;</span>&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ProcID&nbsp;=&nbsp;Form1.TextBox2.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''TextBox1.Text&nbsp;=&nbsp;ProcID</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;ProcI''D&nbsp;=&nbsp;'Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;ProcID</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''c&nbsp;=&nbsp;TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;TextBox2.Text&nbsp;=&nbsp;Form1.TextBox3.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''MsgBox(c)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''AppActivate(c)</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;123qweasdzxc&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;%c&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKe'ys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;123qweasdzxc&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;%FO&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''My.Computer.Keyboard.SendKeys(&quot;%F&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''My.Computer.Keyboard.SendKeys(&quot;{TAB}&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;PhoneBook.txt&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;PhoneBook.txt&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;{TAB}&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;PhoneBook.txt&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''My.Computer.Keyboard.SendKeys(&quot;%F&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''My.Computer.Keyboard.SendKeys(&quot;{TAB}&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;{TAB}&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;{TAB}&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;&#43;O&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;&#43;N&quot;,&nbsp;True)</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;&#43;N&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;&#43;F&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyb'oard.SendKeys(&quot;{TAB}&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;{TAB}&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''My.Computer.Keyboard.SendKeys(&quot;^C&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''My.Computer.Keyboard.SendKeys(&quot;^c&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''My.Computer.Keyboard.SendKeys(&quot;^c&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''My.Computer.Keyboard.SendKeys(&quot;^c&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''My.Computer.Keyboard.SendKeys(&quot;^c&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''My.Computer.Keyboard.SendKeys(&quot;^c&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Me.Top&nbsp;=&nbsp;False</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''Me.Show()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''Me.Select()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''txtDataReceived.Clear()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''txtDataReceived.Paste()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Me.Show()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;<span class="skype_c2c_print_container skype_c2c notranslate">006583642487</span><span id="skype_c2c_container" class="skype_c2c_container skype_c2c notranslate" dir="ltr"><span class="skype_c2c_highlighting_inactive_common" dir="ltr"><span id="non_free_num_ui" class="skype_c2c_textarea_span"><img class="skype_c2c_logo_img" alt="" width="0" height="0"><span class="skype_c2c_text_span">006583642487</span><span class="skype_c2c_free_text_span">&nbsp;</span></span></span></span>&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(d,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;%&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;%al&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;%F&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;<span class="skype_c2c_print_container skype_c2c notranslate">006591737839</span><span id="skype_c2c_container" class="skype_c2c_container skype_c2c notranslate" dir="ltr"><span class="skype_c2c_highlighting_inactive_common" dir="ltr"><span id="non_free_num_ui" class="skype_c2c_textarea_span"><img class="skype_c2c_logo_img" alt="" width="0" height="0"><span class="skype_c2c_text_span">006591737839</span></span></span></span>&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Else</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;End&nbsp;If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'GoTo&nbsp;Pause</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''Form2.TopMost()&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ProcID&nbsp;=&nbsp;Shell(&quot;C:\Program&nbsp;Files\Voxox\Vovox.EXE&quot;,&nbsp;AppWinStyle.NormalFocus)</span>&nbsp;
&nbsp;
&nbsp;
errorhandler:&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Exit</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;ListBox1_SelectedIndexChanged(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;ListBox1.SelectedIndexChanged&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Text&nbsp;=&nbsp;ListBox1.SelectedItem&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox3.Text&nbsp;=&nbsp;ListBox1.SelectedItem&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;Imports&nbsp;System</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Imports&nbsp;System.IO</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Users1\WindowsHome\Documents\</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Class</span>&nbsp;DirAppend&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Public</span>&nbsp;<span class="visualBasic__keyword">Shared</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Main()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Using</span>&nbsp;w&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;StreamWriter&nbsp;=&nbsp;File.AppendText(<span class="visualBasic__string">&quot;F:\PhoneBook.txt&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Log(<span class="visualBasic__string">&quot;Test1&quot;</span>,&nbsp;w)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Log(<span class="visualBasic__string">&quot;Test2&quot;</span>,&nbsp;w)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Using</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Users1\WindowsHome\Documents\</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Using</span>&nbsp;r&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;StreamReader&nbsp;=&nbsp;File.OpenText(<span class="visualBasic__string">&quot;F:\PhoneBook.txt&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;DumpLog(r)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Using</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Public</span>&nbsp;<span class="visualBasic__keyword">Shared</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Log(<span class="visualBasic__keyword">ByVal</span>&nbsp;logMessage&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">String</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;w&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;TextWriter)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;w.Write(vbCrLf&nbsp;&#43;&nbsp;<span class="visualBasic__string">&quot;Log&nbsp;Entry&nbsp;:&nbsp;&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;w.WriteLine(<span class="visualBasic__string">&quot;{0}&nbsp;{1}&quot;</span>,&nbsp;DateTime.Now.ToLongTimeString(),&nbsp;_&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;DateTime.Now.ToLongDateString())&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;w.WriteLine(<span class="visualBasic__string">&quot;&nbsp;&nbsp;:&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;w.WriteLine(<span class="visualBasic__string">&quot;&nbsp;&nbsp;:{0}&quot;</span>,&nbsp;logMessage)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;w.WriteLine(<span class="visualBasic__string">&quot;-------------------------------&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Public</span>&nbsp;<span class="visualBasic__keyword">Shared</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;DumpLog(<span class="visualBasic__keyword">ByVal</span>&nbsp;r&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;StreamReader)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">On</span>&nbsp;<span class="visualBasic__keyword">Error</span>&nbsp;<span class="visualBasic__keyword">GoTo</span>&nbsp;errorhandler&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;line&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">String</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;i&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">For</span>&nbsp;i&nbsp;=&nbsp;<span class="visualBasic__number">1</span>&nbsp;<span class="visualBasic__keyword">To</span>&nbsp;<span class="visualBasic__number">100</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;line&nbsp;=&nbsp;r.ReadLine()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Forms.Form1.ListBox1.Items.Add(line)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Next</span>&nbsp;i&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">While</span>&nbsp;<span class="visualBasic__keyword">Not</span>&nbsp;(line&nbsp;<span class="visualBasic__keyword">Is</span>&nbsp;<span class="visualBasic__keyword">Nothing</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.WriteLine(line)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;line&nbsp;=&nbsp;r.ReadLine()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;My.Forms.Form1.ListBox1.Items.Add(line)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">While</span>&nbsp;
errorhandler:&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Exit</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Class</span>&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Button10_Click(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;Button10.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;d&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;c&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;d&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Shell(<span class="visualBasic__string">&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;</span>,&nbsp;AppWinStyle.NormalFocus)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;c&nbsp;=&nbsp;&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Forms.Form1.Button10.&nbsp;&nbsp;&nbsp;&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Me.TopMost&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ProcID&nbsp;=&nbsp;Form1.TextBox2.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Form1a.TextBox1.Text&nbsp;=&nbsp;ProcID&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox1.Text&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;ProcID&nbsp;=&nbsp;&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;ProcID</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;On&nbsp;Error&nbsp;GoTo&nbsp;errorhandler</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c&nbsp;=&nbsp;TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;Form1a.TextBox3.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(<span class="visualBasic__string">&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%S&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%FOn&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'AppActivate(&quot;Open&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%n&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;1.wma&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;~&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%P&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;P&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''&nbsp;My.Computer.Keyboard.SendKeys(&quot;^P&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;<span class="skype_c2c_print_container skype_c2c notranslate">006591737839</span><span id="skype_c2c_container" class="skype_c2c_container skype_c2c notranslate" dir="ltr"><span class="skype_c2c_highlighting_inactive_common" dir="ltr"><span id="non_free_num_ui" class="skype_c2c_textarea_span"><img class="skype_c2c_logo_img" alt="" width="0" height="0"><span class="skype_c2c_text_span">006591737839</span></span></span></span>&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(<span class="visualBasic__string">&quot;1&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Button11_Click(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;Button11.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;d&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;c&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;d&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Shell(<span class="visualBasic__string">&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;</span>,&nbsp;AppWinStyle.NormalFocus)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;c&nbsp;=&nbsp;&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Me.TopMost&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ProcID&nbsp;=&nbsp;Form1.TextBox2.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Form1a.TextBox1.Text&nbsp;=&nbsp;ProcID&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox1.Text&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;ProcID&nbsp;=&nbsp;&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;ProcID</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;On&nbsp;Error&nbsp;GoTo&nbsp;errorhandler</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c&nbsp;=&nbsp;TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;Form1a.TextBox3.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(<span class="visualBasic__string">&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%S&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%FOn&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'AppActivate(&quot;Open&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%n&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;2.wma&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;~&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%P&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;P&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''&nbsp;My.Computer.Keyboard.SendKeys(&quot;^P&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;<span class="skype_c2c_print_container skype_c2c notranslate">006591737839</span><span id="skype_c2c_container" class="skype_c2c_container skype_c2c notranslate" dir="ltr"><span class="skype_c2c_highlighting_inactive_common" dir="ltr"><span id="non_free_num_ui" class="skype_c2c_textarea_span"><img class="skype_c2c_logo_img" alt="" width="0" height="0"><span class="skype_c2c_text_span">006591737839</span></span></span></span>&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(<span class="visualBasic__string">&quot;2&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Button12_Click(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;Button12.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;d&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;c&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;d&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Shell(<span class="visualBasic__string">&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;</span>,&nbsp;AppWinStyle.NormalFocus)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;c&nbsp;=&nbsp;&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Me.TopMost&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ProcID&nbsp;=&nbsp;Form1.TextBox2.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Form1a.TextBox1.Text&nbsp;=&nbsp;ProcID&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox1.Text&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;ProcID&nbsp;=&nbsp;&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;ProcID</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;On&nbsp;Error&nbsp;GoTo&nbsp;errorhandler</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c&nbsp;=&nbsp;TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;Form1a.TextBox3.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(<span class="visualBasic__string">&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%S&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%FOn&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'AppActivate(&quot;Open&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%n&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;3.wma&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;~&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%P&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;P&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''&nbsp;My.Computer.Keyboard.SendKeys(&quot;^P&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;<span class="skype_c2c_print_container skype_c2c notranslate">006591737839</span><span id="skype_c2c_container" class="skype_c2c_container skype_c2c notranslate" dir="ltr"><span class="skype_c2c_highlighting_inactive_common" dir="ltr"><span id="non_free_num_ui" class="skype_c2c_textarea_span"><img class="skype_c2c_logo_img" alt="" width="0" height="0"><span class="skype_c2c_text_span">006591737839</span></span></span></span>&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(<span class="visualBasic__string">&quot;3&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Button13_Click(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;Button13.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;d&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;c&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;d&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Shell(<span class="visualBasic__string">&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;</span>,&nbsp;AppWinStyle.NormalFocus)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;c&nbsp;=&nbsp;&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Me.TopMost&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ProcID&nbsp;=&nbsp;Form1.TextBox2.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Form1a.TextBox1.Text&nbsp;=&nbsp;ProcID&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox1.Text&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;ProcID&nbsp;=&nbsp;&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;ProcID</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;On&nbsp;Error&nbsp;GoTo&nbsp;errorhandler</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c&nbsp;=&nbsp;TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;Form1a.TextBox3.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(<span class="visualBasic__string">&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%S&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%FOn&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'AppActivate(&quot;Open&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%n&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;4.wma&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;~&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%P&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;P&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''&nbsp;My.Computer.Keyboard.SendKeys(&quot;^P&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;<span class="skype_c2c_print_container skype_c2c notranslate">006591737839</span><span id="skype_c2c_container" class="skype_c2c_container skype_c2c notranslate" dir="ltr"><span class="skype_c2c_highlighting_inactive_common" dir="ltr"><span id="non_free_num_ui" class="skype_c2c_textarea_span"><img class="skype_c2c_logo_img" alt="" width="0" height="0"><span class="skype_c2c_text_span">006591737839</span></span></span></span>&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(<span class="visualBasic__string">&quot;4&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Button14_Click(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;Button14.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;d&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;c&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;d&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Shell(<span class="visualBasic__string">&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;</span>,&nbsp;AppWinStyle.NormalFocus)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;c&nbsp;=&nbsp;&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Me.TopMost&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ProcID&nbsp;=&nbsp;Form1.TextBox2.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Form1a.TextBox1.Text&nbsp;=&nbsp;ProcID&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox1.Text&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;ProcID&nbsp;=&nbsp;&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;ProcID</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;On&nbsp;Error&nbsp;GoTo&nbsp;errorhandler</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c&nbsp;=&nbsp;TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;Form1a.TextBox3.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(<span class="visualBasic__string">&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%S&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%FOn&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'AppActivate(&quot;Open&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%n&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;5.wma&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;~&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%P&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;P&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''&nbsp;My.Computer.Keyboard.SendKeys(&quot;^P&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;<span class="skype_c2c_print_container skype_c2c notranslate">006591737839</span><span id="skype_c2c_container" class="skype_c2c_container skype_c2c notranslate" dir="ltr"><span class="skype_c2c_highlighting_inactive_common" dir="ltr"><span id="non_free_num_ui" class="skype_c2c_textarea_span"><img class="skype_c2c_logo_img" alt="" width="0" height="0"><span class="skype_c2c_text_span">006591737839</span></span></span></span>&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(<span class="visualBasic__string">&quot;5&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Button15_Click(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;Button15.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;d&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;c&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;d&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Shell(<span class="visualBasic__string">&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;</span>,&nbsp;AppWinStyle.NormalFocus)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;c&nbsp;=&nbsp;&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Me.TopMost&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ProcID&nbsp;=&nbsp;Form1.TextBox2.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Form1a.TextBox1.Text&nbsp;=&nbsp;ProcID&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox1.Text&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;ProcID&nbsp;=&nbsp;&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;ProcID</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;On&nbsp;Error&nbsp;GoTo&nbsp;errorhandler</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c&nbsp;=&nbsp;TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;Form1a.TextBox3.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(<span class="visualBasic__string">&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%S&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%FOn&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'AppActivate(&quot;Open&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%n&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;6.wma&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;~&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%P&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;P&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''&nbsp;My.Computer.Keyboard.SendKeys(&quot;^P&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;<span class="skype_c2c_print_container skype_c2c notranslate">006591737839</span><span id="skype_c2c_container" class="skype_c2c_container skype_c2c notranslate" dir="ltr"><span class="skype_c2c_highlighting_inactive_common" dir="ltr"><span id="non_free_num_ui" class="skype_c2c_textarea_span"><img class="skype_c2c_logo_img" alt="" width="0" height="0"><span class="skype_c2c_text_span">006591737839</span></span></span></span>&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(<span class="visualBasic__string">&quot;6&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Button16_Click(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;Button16.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;d&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;c&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;d&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Shell(<span class="visualBasic__string">&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;</span>,&nbsp;AppWinStyle.NormalFocus)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;c&nbsp;=&nbsp;&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Me.TopMost&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ProcID&nbsp;=&nbsp;Form1.TextBox2.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Form1a.TextBox1.Text&nbsp;=&nbsp;ProcID&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox1.Text&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;ProcID&nbsp;=&nbsp;&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;ProcID</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;On&nbsp;Error&nbsp;GoTo&nbsp;errorhandler</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c&nbsp;=&nbsp;TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;Form1a.TextBox3.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(<span class="visualBasic__string">&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%S&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%FOn&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'AppActivate(&quot;Open&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%n&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;7.wma&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;~&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%P&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;P&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''&nbsp;My.Computer.Keyboard.SendKeys(&quot;^P&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;<span class="skype_c2c_print_container skype_c2c notranslate">006591737839</span><span id="skype_c2c_container" class="skype_c2c_container skype_c2c notranslate" dir="ltr"><span class="skype_c2c_highlighting_inactive_common" dir="ltr"><span id="non_free_num_ui" class="skype_c2c_textarea_span"><img class="skype_c2c_logo_img" alt="" width="0" height="0"><span class="skype_c2c_text_span">006591737839</span></span></span></span>&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(<span class="visualBasic__string">&quot;7&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Button17_Click(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;Button17.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;d&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;c&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;d&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Shell(<span class="visualBasic__string">&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;</span>,&nbsp;AppWinStyle.NormalFocus)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;c&nbsp;=&nbsp;&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Me.TopMost&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ProcID&nbsp;=&nbsp;Form1.TextBox2.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Form1a.TextBox1.Text&nbsp;=&nbsp;ProcID&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox1.Text&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;ProcID&nbsp;=&nbsp;&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;ProcID</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;On&nbsp;Error&nbsp;GoTo&nbsp;errorhandler</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c&nbsp;=&nbsp;TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;Form1a.TextBox3.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(<span class="visualBasic__string">&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%S&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%FOn&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'AppActivate(&quot;Open&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%n&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;8.wma&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;~&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%P&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;P&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''&nbsp;My.Computer.Keyboard.SendKeys(&quot;^P&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;<span class="skype_c2c_print_container skype_c2c notranslate">006591737839</span><span id="skype_c2c_container" class="skype_c2c_container skype_c2c notranslate" dir="ltr"><span class="skype_c2c_highlighting_inactive_common" dir="ltr"><span id="non_free_num_ui" class="skype_c2c_textarea_span"><img class="skype_c2c_logo_img" alt="" width="0" height="0"><span class="skype_c2c_text_span">006591737839</span></span></span></span>&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(<span class="visualBasic__string">&quot;8&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Button18_Click(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;Button18.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;d&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;c&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;d&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Shell(<span class="visualBasic__string">&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;</span>,&nbsp;AppWinStyle.NormalFocus)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;c&nbsp;=&nbsp;&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Me.TopMost&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ProcID&nbsp;=&nbsp;Form1.TextBox2.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Form1a.TextBox1.Text&nbsp;=&nbsp;ProcID&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox1.Text&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;ProcID&nbsp;=&nbsp;&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;ProcID</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;On&nbsp;Error&nbsp;GoTo&nbsp;errorhandler</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c&nbsp;=&nbsp;TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;Form1a.TextBox3.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(<span class="visualBasic__string">&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%S&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%FOn&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'AppActivate(&quot;Open&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%n&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;9.wma&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;~&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%P&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;P&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''&nbsp;My.Computer.Keyboard.SendKeys(&quot;^P&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;<span class="skype_c2c_print_container skype_c2c notranslate">006591737839</span><span id="skype_c2c_container" class="skype_c2c_container skype_c2c notranslate" dir="ltr"><span class="skype_c2c_highlighting_inactive_common" dir="ltr"><span id="non_free_num_ui" class="skype_c2c_textarea_span"><img class="skype_c2c_logo_img" alt="" width="0" height="0"><span class="skype_c2c_text_span">006591737839</span></span></span></span>&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(<span class="visualBasic__string">&quot;9&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Button19_Click(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;Button19.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;d&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;c&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;d&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Shell(<span class="visualBasic__string">&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;</span>,&nbsp;AppWinStyle.NormalFocus)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;c&nbsp;=&nbsp;&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Me.TopMost&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ProcID&nbsp;=&nbsp;Form1.TextBox2.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Form1a.TextBox1.Text&nbsp;=&nbsp;ProcID&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox1.Text&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;ProcID&nbsp;=&nbsp;&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;ProcID</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;On&nbsp;Error&nbsp;GoTo&nbsp;errorhandler</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c&nbsp;=&nbsp;TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;Form1a.TextBox3.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(<span class="visualBasic__string">&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(<span class="visualBasic__string">&quot;0&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%S&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%FOn&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'AppActivate(&quot;Open&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%n&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;0.wma&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;~&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%P&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;P&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''&nbsp;My.Computer.Keyboard.SendKeys(&quot;^P&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;<span class="skype_c2c_print_container skype_c2c notranslate">006591737839</span><span id="skype_c2c_container" class="skype_c2c_container skype_c2c notranslate" dir="ltr"><span class="skype_c2c_highlighting_inactive_common" dir="ltr"><span id="non_free_num_ui" class="skype_c2c_textarea_span"><img class="skype_c2c_logo_img" alt="" width="0" height="0"><span class="skype_c2c_text_span">006591737839</span></span></span></span>&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;TextBox2_TextChanged(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;TextBox2.TextChanged&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;txtDataReceived.Text&nbsp;=&nbsp;TextBox2.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Button20_Click(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;Button20.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;d&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;c&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;d&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Shell(<span class="visualBasic__string">&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;</span>,&nbsp;AppWinStyle.NormalFocus)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;c&nbsp;=&nbsp;&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Me.TopMost&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ProcID&nbsp;=&nbsp;Form1.TextBox2.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Form1a.TextBox1.Text&nbsp;=&nbsp;ProcID&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox1.Text&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;ProcID&nbsp;=&nbsp;&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;ProcID</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;On&nbsp;Error&nbsp;GoTo&nbsp;errorhandler</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c&nbsp;=&nbsp;TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;Form1a.TextBox3.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(<span class="visualBasic__string">&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(<span class="visualBasic__string">&quot;*&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%S&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%FOn&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'AppActivate(&quot;Open&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%n&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;star.wma&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;~&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%P&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;P&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''&nbsp;My.Computer.Keyboard.SendKeys(&quot;^P&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;<span class="skype_c2c_print_container skype_c2c notranslate">006591737839</span><span id="skype_c2c_container" class="skype_c2c_container skype_c2c notranslate" dir="ltr"><span class="skype_c2c_highlighting_inactive_common" dir="ltr"><span id="non_free_num_ui" class="skype_c2c_textarea_span"><img class="skype_c2c_logo_img" alt="" width="0" height="0"><span class="skype_c2c_text_span">006591737839</span></span></span></span>&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Button21_Click(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;Button21.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;d&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;c&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;d&nbsp;As&nbsp;Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Shell(<span class="visualBasic__string">&quot;C:\Windows.old.002\Windows\Windows\winsxs\x86_microsoft-windows-mediaplayer-core_31bf3856ad364e35_6.0.6000.16386_none_09330123522ea8c1\wmplayer.exe&quot;</span>,&nbsp;AppWinStyle.NormalFocus)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;c&nbsp;=&nbsp;&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;a&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Me.TopMost&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ProcID&nbsp;=&nbsp;Form1.TextBox2.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Form1a.TextBox1.Text&nbsp;=&nbsp;ProcID&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox1.Text&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Form1a.TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;ProcID&nbsp;=&nbsp;&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;ProcID</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;On&nbsp;Error&nbsp;GoTo&nbsp;errorhandler</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c&nbsp;=&nbsp;TextBox1.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox2.Text&nbsp;=&nbsp;Form1a.TextBox3.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(<span class="visualBasic__string">&quot;Windows&nbsp;Media&nbsp;Player&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(<span class="visualBasic__string">&quot;#&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%S&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%FOn&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'AppActivate(&quot;Open&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%n&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;has.wma&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;~&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;%P&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;#&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''&nbsp;My.Computer.Keyboard.SendKeys(&quot;^P&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;<span class="skype_c2c_print_container skype_c2c notranslate">006591737839</span><span id="skype_c2c_container" class="skype_c2c_container skype_c2c notranslate" dir="ltr"><span class="skype_c2c_highlighting_inactive_common" dir="ltr"><span id="non_free_num_ui" class="skype_c2c_textarea_span"><img class="skype_c2c_logo_img" alt="" width="0" height="0"><span class="skype_c2c_text_span">006591737839</span></span></span></span>&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(<span class="visualBasic__string">&quot;#&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Public</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;<span class="visualBasic__keyword">New</span>()&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;This&nbsp;call&nbsp;is&nbsp;required&nbsp;by&nbsp;the&nbsp;Windows&nbsp;Form&nbsp;Designer.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;InitializeComponent()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Me</span>.TopMost&nbsp;=&nbsp;<span class="visualBasic__keyword">True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Add&nbsp;any&nbsp;initialization&nbsp;after&nbsp;the&nbsp;InitializeComponent()&nbsp;call.</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Button22_Click(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;Button22.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID1&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;a&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;d1&nbsp;As&nbsp;String</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;e1a&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Start&nbsp;the&nbsp;Calculator&nbsp;application,&nbsp;and&nbsp;store&nbsp;the&nbsp;process&nbsp;id.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;On&nbsp;Error&nbsp;GoTo&nbsp;errorhandler</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'GoTo&nbsp;Pause</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''Form2.Show()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;If&nbsp;TextBox5.Text&nbsp;=&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;Shell(<span class="visualBasic__string">&quot;C:\Program&nbsp;Files\Skype\Phone\Skype.exe&quot;</span>,&nbsp;AppWinStyle.NormalFocus)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID1&nbsp;=&nbsp;Shell(<span class="visualBasic__string">&quot;C:\Windows\System32\SoundRecorder.exe&quot;</span>,&nbsp;AppWinStyle.NormalFocus)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Skype.Show()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Skype.TopMost&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox3.Text&nbsp;=&nbsp;ListBox1.SelectedItem</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'If&nbsp;Skype.TextBox1.Text&nbsp;=&nbsp;TextBox1.Text&nbsp;Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Skype.Show()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;End&nbsp;If</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;c&nbsp;=&nbsp;&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox2.Text&nbsp;=&nbsp;&quot;0&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Me</span>.TopMost&nbsp;=&nbsp;<span class="visualBasic__keyword">True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;ProcID&nbsp;=&nbsp;Form1.TextBox2.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;TextBox1.Text&nbsp;=&nbsp;ProcID</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'AppActivate(ProcID)</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox2.Text&nbsp;=&nbsp;ProcID1</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MsgBox(ProcID1)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;ProcID&nbsp;=&nbsp;'Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;ProcID</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'c&nbsp;=&nbsp;TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox1.Text&nbsp;=&nbsp;Form1.TextBox1.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;TextBox2.Text&nbsp;=&nbsp;Form1.TextBox3.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID1)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'AppActivate(ProcID1)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox4.Text&nbsp;=&nbsp;ProcID&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MsgBox(ProcID)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'MsgBox(ProcID)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(ProcID)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%a&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;l&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%a&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%l&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__keyword">Me</span>.TextBox5.Text,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%a&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%l&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;123qweasdzxc&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;~&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;123qweasdzxc&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;<span class="skype_c2c_print_container skype_c2c notranslate">006591737839</span><span id="skype_c2c_container" class="skype_c2c_container skype_c2c notranslate" dir="ltr"><span class="skype_c2c_highlighting_inactive_common" dir="ltr"><span id="non_free_num_ui" class="skype_c2c_textarea_span"><img class="skype_c2c_logo_img" alt="" width="0" height="0"><span class="skype_c2c_text_span">006591737839</span></span></span></span>&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(txtDataReceived.Text,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(d,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;%&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;%al&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;%F&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(&quot;<span class="skype_c2c_print_container skype_c2c notranslate">006591737839</span><span id="skype_c2c_container" class="skype_c2c_container skype_c2c notranslate" dir="ltr"><span class="skype_c2c_highlighting_inactive_common" dir="ltr"><span id="non_free_num_ui" class="skype_c2c_textarea_span"><img class="skype_c2c_logo_img" alt="" width="0" height="0"><span class="skype_c2c_text_span">006591737839</span></span></span></span>&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Else</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;End&nbsp;If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'GoTo&nbsp;Pause</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">''Form2.TopMost()&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'ProcID&nbsp;=&nbsp;Shell(&quot;C:\Program&nbsp;Files\Voxox\Vovox.EXE&quot;,&nbsp;AppWinStyle.NormalFocus)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;Else</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;Exit&nbsp;Sub</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;End&nbsp;If</span>&nbsp;
&nbsp;
errorhandler:&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Exit</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Shared</span>&nbsp;aTimer&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.Timers.Timer&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Public</span>&nbsp;<span class="visualBasic__keyword">Shared</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Main()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Normally,&nbsp;the&nbsp;timer&nbsp;is&nbsp;declared&nbsp;at&nbsp;the&nbsp;class&nbsp;level,&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;so&nbsp;that&nbsp;it&nbsp;stays&nbsp;in&nbsp;scope&nbsp;as&nbsp;long&nbsp;as&nbsp;it&nbsp;is&nbsp;needed.&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;If&nbsp;the&nbsp;timer&nbsp;is&nbsp;declared&nbsp;in&nbsp;a&nbsp;long-running&nbsp;method,&nbsp;&nbsp;&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;KeepAlive&nbsp;must&nbsp;be&nbsp;used&nbsp;to&nbsp;prevent&nbsp;the&nbsp;JIT&nbsp;compiler&nbsp;&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;from&nbsp;allowing&nbsp;aggressive&nbsp;garbage&nbsp;collection&nbsp;to&nbsp;occur&nbsp;&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;before&nbsp;the&nbsp;method&nbsp;ends.&nbsp;You&nbsp;can&nbsp;experiment&nbsp;with&nbsp;this&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;by&nbsp;commenting&nbsp;out&nbsp;the&nbsp;class-level&nbsp;declaration&nbsp;and&nbsp;&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;uncommenting&nbsp;the&nbsp;declaration&nbsp;below;&nbsp;then&nbsp;uncomment&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;the&nbsp;GC.KeepAlive(aTimer)&nbsp;at&nbsp;the&nbsp;end&nbsp;of&nbsp;the&nbsp;method.&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Dim&nbsp;aTimer&nbsp;As&nbsp;System.Timers.Timer&nbsp;</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Create&nbsp;a&nbsp;timer&nbsp;with&nbsp;a&nbsp;ten&nbsp;second&nbsp;interval.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;aTimer&nbsp;=&nbsp;<span class="visualBasic__keyword">New</span>&nbsp;System.Timers.Timer(<span class="visualBasic__number">10000</span>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Hook&nbsp;up&nbsp;the&nbsp;Elapsed&nbsp;event&nbsp;for&nbsp;the&nbsp;timer.&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;AddHandler&nbsp;aTimer.Elapsed,&nbsp;AddressOf&nbsp;OnTimedEvent</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Set&nbsp;the&nbsp;Interval&nbsp;to&nbsp;2&nbsp;seconds&nbsp;(2000&nbsp;milliseconds).</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;aTimer.Interval&nbsp;=&nbsp;<span class="visualBasic__number">2000</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;aTimer.Enabled&nbsp;=&nbsp;<span class="visualBasic__keyword">True</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Console.WriteLine(&quot;Press&nbsp;the&nbsp;Enter&nbsp;key&nbsp;to&nbsp;exit&nbsp;the&nbsp;program.&quot;)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Console.ReadLine()</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;If&nbsp;the&nbsp;timer&nbsp;is&nbsp;declared&nbsp;in&nbsp;a&nbsp;long-running&nbsp;method,&nbsp;use&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;KeepAlive&nbsp;to&nbsp;prevent&nbsp;garbage&nbsp;collection&nbsp;from&nbsp;occurring&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;before&nbsp;the&nbsp;method&nbsp;ends.&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'GC.KeepAlive(aTimer)&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;OnTimedEvent(source&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Object</span>,&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;ElapsedEventArgs)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Console.WriteLine(&quot;The&nbsp;Elapsed&nbsp;event&nbsp;was&nbsp;raised&nbsp;at&nbsp;{0}&quot;,&nbsp;e.SignalTime)</span>&nbsp;
&nbsp;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;TextBox3_DoubleClick(sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Object</span>,&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;TextBox3.DoubleClick&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'End&nbsp;Class</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;TextBox3_MouseDoubleClick(sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Object</span>,&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;MouseEventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;TextBox3.MouseDoubleClick&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;TextBox3.Clear()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;i,&nbsp;n,&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;aTimer&nbsp;=&nbsp;<span class="visualBasic__keyword">New</span>&nbsp;System.Timers.Timer(<span class="visualBasic__number">10000</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">For</span>&nbsp;i&nbsp;=&nbsp;<span class="visualBasic__number">0</span>&nbsp;<span class="visualBasic__keyword">To</span>&nbsp;<span class="visualBasic__number">9</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;Dim&nbsp;msg&nbsp;=&nbsp;&quot;Do&nbsp;you&nbsp;want&nbsp;to&nbsp;continue?&quot;</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Display&nbsp;a&nbsp;simple&nbsp;message&nbsp;box.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;MsgBox(msg)</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Define&nbsp;a&nbsp;title&nbsp;for&nbsp;the&nbsp;message&nbsp;box.&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;Dim&nbsp;title&nbsp;=&nbsp;&quot;MsgBox&nbsp;Demonstration&quot;</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Add&nbsp;the&nbsp;title&nbsp;to&nbsp;the&nbsp;display.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MsgBox(msg,&nbsp;,&nbsp;i)</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Now&nbsp;define&nbsp;a&nbsp;style&nbsp;for&nbsp;the&nbsp;message&nbsp;box.&nbsp;In&nbsp;this&nbsp;example,&nbsp;the&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;message&nbsp;box&nbsp;will&nbsp;have&nbsp;Yes&nbsp;and&nbsp;No&nbsp;buttons,&nbsp;the&nbsp;default&nbsp;will&nbsp;be&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;the&nbsp;No&nbsp;button,&nbsp;and&nbsp;a&nbsp;Critical&nbsp;Message&nbsp;icon&nbsp;will&nbsp;be&nbsp;present.&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;style&nbsp;=&nbsp;MsgBoxStyle.YesNo&nbsp;<span class="visualBasic__keyword">Or</span>&nbsp;MsgBoxStyle.DefaultButton2&nbsp;<span class="visualBasic__keyword">Or</span>&nbsp;_&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MsgBoxStyle.Critical&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Display&nbsp;the&nbsp;message&nbsp;box&nbsp;and&nbsp;save&nbsp;the&nbsp;response,&nbsp;Yes&nbsp;or&nbsp;No.&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;response&nbsp;=&nbsp;MsgBox(i,&nbsp;style,&nbsp;i)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Take&nbsp;some&nbsp;action&nbsp;based&nbsp;on&nbsp;the&nbsp;response.&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;response&nbsp;=&nbsp;MsgBoxResult.Yes&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.AppendText(<span class="visualBasic__string">&quot;&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;MsgBox(&quot;YES,&nbsp;continue!!&quot;,&nbsp;,&nbsp;title)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox3.AppendText(i)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;response&nbsp;=&nbsp;MsgBoxResult.No&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;MsgBox(&quot;NO,&nbsp;stop!!&quot;,&nbsp;,&nbsp;title)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox3.AppendText(<span class="visualBasic__string">&quot;&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Hook&nbsp;up&nbsp;the&nbsp;Elapsed&nbsp;event&nbsp;for&nbsp;the&nbsp;timer.&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;AddHandler&nbsp;aTimer.Elapsed,&nbsp;AddressOf&nbsp;OnTimedEvent</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Set&nbsp;the&nbsp;Interval&nbsp;to&nbsp;2&nbsp;seconds&nbsp;(2000&nbsp;milliseconds).</span>&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'For&nbsp;n&nbsp;=&nbsp;1&nbsp;To&nbsp;1</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Button24.PerformClick()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;TextBox3.Text&nbsp;=&nbsp;i</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;Timer2.Interval&nbsp;=&nbsp;2000</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;Timer2.Enabled&nbsp;=&nbsp;True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;Timer2.Start()</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'a:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;If&nbsp;Timer2.ToString&nbsp;=&nbsp;&quot;0000&quot;&nbsp;Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Stop</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;MsgBox(i)</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;If&nbsp;Keys.I&nbsp;Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'handler:</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;If&nbsp;MsgBox(i,&nbsp;MsgBoxStyle.YesNo,&nbsp;MsgBoxResult.Yes)&nbsp;Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;If&nbsp;MsgBox(i,&nbsp;MsgBoxResult.Yes)&nbsp;Then</span>&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Else</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;ElseIf&nbsp;MsgBoxResult.Yes&nbsp;=&nbsp;6&nbsp;Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;TextBox3.AppendText(&quot;&quot;)</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;End&nbsp;If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Next</span>&nbsp;i&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'End&nbsp;If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Exit</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Else</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;GoTo&nbsp;a</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;End&nbsp;If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Else</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;Exit&nbsp;Sub</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;End&nbsp;If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Me</span>.TopMost&nbsp;=&nbsp;<span class="visualBasic__keyword">True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Timer2.<span class="visualBasic__keyword">Stop</span>()&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;If&nbsp;txtDataReceived.Text&nbsp;=&nbsp;&quot;101&quot;&nbsp;Then</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;Else</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;End&nbsp;If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;&nbsp;&nbsp;Next&nbsp;n</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Next&nbsp;i</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;GoTo&nbsp;handler</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;TextBox3_TextChanged(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;TextBox3.TextChanged&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;TextBox4_TextChanged(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;TextBox4.TextChanged&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Button23_Click(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;Button23.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox3.Text&nbsp;=&nbsp;ListBox1.SelectedItem</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;TextBox4.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(ProcID)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%a&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;l&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%a&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%l&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__keyword">Me</span>.TextBox5.Text,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%a&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%l&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;123qweasdzxc&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;~&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;TextBox5.Clear()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Button24_Click(sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Object</span>,&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;Button24.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtDataReceived.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;TextBox5_MouseDoubleClick(sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Object</span>,&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;MouseEventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;TextBox5.MouseDoubleClick&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.Text&nbsp;=&nbsp;txtDataReceived.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;TextBox5_TextChanged(sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Object</span>,&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;TextBox5.TextChanged&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;If&nbsp;txtDataReceived.Text&nbsp;=&nbsp;&quot;&#43;&quot;&nbsp;Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Button23.PerformClick()</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;txtDataReceived.Text&nbsp;=&nbsp;&quot;101&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;End&nbsp;If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;TextBox5.Text&nbsp;=&nbsp;txtDataReceived.Text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;TextBox5.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;!P&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;TextBox5.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;!#P&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;TextBox5.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;P&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;TextBox5.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;#&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;TextBox5.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;!&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ElseIf</span>&nbsp;TextBox5.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;&#43;&quot;</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox6.AppendText(TextBox5.Text)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Button25_Click(sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Object</span>,&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;Button25.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox3.Text&nbsp;=&nbsp;ListBox1.SelectedItem</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;TextBox4.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(ProcID)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%S&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;S&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;%S&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;S&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;%{PGDN}&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;%a&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;%l&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(Me.TextBox5.Text,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(&quot;%a&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(&quot;%l&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;123qweasdzxc&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Button26_Click(sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Object</span>,&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;Button26.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox3.Text&nbsp;=&nbsp;ListBox1.SelectedItem</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;TextBox4.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(ProcID)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;123qweasdzxc&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;~&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;TextBox6_TextChanged(sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Object</span>,&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;TextBox6.TextChanged&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Button27_Click(sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Object</span>,&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;Button27.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ProcID&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'TextBox3.Text&nbsp;=&nbsp;ListBox1.SelectedItem</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;TextBox4.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(ProcID)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcID&nbsp;=&nbsp;TextBox4.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppActivate(ProcID)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;a&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(<span class="visualBasic__string">&quot;&#43;=&quot;</span>,&nbsp;<span class="visualBasic__keyword">True</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;%a%a&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;%&#43;a&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;%a&quot;,&nbsp;True)</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;%&#43;a&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;&nbsp;My.Computer.Keyboard.SendKeys(&quot;%a&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;My.Computer.Keyboard.SendKeys(&quot;a&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;a&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'My.Computer.Keyboard.SendKeys(&quot;~&quot;,&nbsp;True)</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextBox5.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Class</span>&nbsp;
<span class="visualBasic__com">'End&nbsp;Class</span></pre>
</div>
</div>
</div>
<h1><span>Source Code Files</span></h1>
<ul>
<li><em>Source Code attached.</em> </li></ul>
<h1>More Information</h1>
<p><em>For more information on Phone Application, please contact <a href="mailto:chanjunthoong@theiet.org">
chanjunthoong@theiet.org</a> or <a href="mailto:chan_junt_hoong@ieee.org">chan_junt_hoong@ieee.org</a>.</em></p>