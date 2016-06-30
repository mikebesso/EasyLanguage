using elsystem;


using elsystem.text;

inputs:
	folder("C:\Users\Mike\Dropbox\Apps\ShinyTrades\ohlc");

var:
	string filename(""),
	string fileinterval(""),
	String extract(""),
	DateTime dt(null),
	DateTime ExtractStartDate(null),
	Bool OK2Write(TRUE),
	String Path(""),
	String FQN("");
	
	


ExtractStartDate = DateTime.Today;

print ("starting: ", ExtractStartDate.ELFormatDate("YYYY-MM-DD"));



if intervaltype = 0 then
	begin
		fileinterval = "T";
		ExtractStartDate = DateTime.Today;
		ExtractStartDate.AddDays(-1);
		
		filename = bardatetime.Format("%Y-%m-%d") & ".csv";

	end
else if intervaltype = 2 then
	begin
		fileinterval = "D";
		ExtractStartDate = DateTime.Create(2012, 1, 1);
		filename = bardatetime.Format("%Y-%m-01") & ".csv";
	end
else if intervaltype = 3 then
	begin
		fileinterval = "W";
		ExtractStartDate = DateTime.Create(2012, 1, 1);
		filename = bardatetime.Format("%Y-01-01") & ".csv";
	end
else if intervaltype = 4 then
	begin
		fileinterval = "M";
		ExtractStartDate = DateTime.Create(2012, 1, 1);
		filename = bardatetime.Format("%Y-01-01") & ".csv";
	end
else if intervaltype = 1 then
	begin

		filename = bardatetime.Format("%Y-%m-01") & ".csv";

		if barinterval = 240 then
			begin
				fileinterval = "4H";
				ExtractStartDate = DateTime.Create(2016, 1, 1);
			end
		else if barinterval = 120 then
			begin
				fileinterval = "2H";
				ExtractStartDate = DateTime.Create(2016, 1, 1);
			end
		else if barinterval = 60 then
			begin
				fileinterval = "H";
				ExtractStartDate = DateTime.Create(2016, 1, 1);
			end
		else
			begin
				fileinterval = numtostr(barinterval, 0) & "m";
				ExtractStartDate = DateTime.Create(2016, 1, 1);
				filename = bardatetime.Format("%Y-%m-%d") & ".csv";
			end;


	end;





If bardatetime >= ExtractStartDate and OK2Write then

begin

	Path = folder & "\" & symbol & "\" & fileinterval & "\";
	
	FQN = Path & symbol & "-" & fileinterval & "-" & filename;
	
PRINT(FQN);			


	try
	
		begin

			
			if FQN <> FQN[1] then 
				begin
					print("New File");
					FileDelete(FQN);
					extract = "timestamp,close,high,low,open,volume" & NewLine;
					FileAppend(FQN, extract);
				end;
			
			If (barstatus(1) = 2) then
			begin
				dt = bardatetime;
				extract = dt.Format("%Y-%m-%dT%H:%M") & ", " 
					& NumToStr(close, 6) & ", " 
					& NumToStr(high, 6) & ", " 
					& NumToStr(low, 6) & ", " 
					& NumToStr(open, 6) & ", " 
					& NumToStr(volume, 0) & NewLine;
				
				FileAppend(FQN, extract);
				
			end;	

			
		end;
		
	catch (exception e)
	
		begin
			OK2Write = FALSE;
			
			Print("Failed to Write: ", FQN);
		end;	
	end;


end;

Plot1(close);
