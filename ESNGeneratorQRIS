import datetime
import csv
from datetime import datetime
from openpyxl import load_workbook

#fungsi konversi list ke sebuah satu kesatuan string
def convert(s):
    # initialization of string to ""
    new = ""
    # traverse in the string
    for x in s:
        new += x 
    # return string
    return new

seperator = ";"
list_baru = []
count = 0
format = "%d/%m/%y"

filename = 'input.txt'
from_input = open(filename,"r+") 
lines = from_input.readlines() # read every lines inside the real QRIS SF

print("\nSelamat datang! \nProgram ini dibuat untuk mempermudah pengerjaan tiket QRIS.")
print("Pastikan pada SF QRIS sudah disiapkan dan direname sebagai input.txt")
next = input("\n  --- Press enter to continue ---")

# Load input txt file
for line in lines :
    line = line.replace('\n',"")
    list_baru.append(line)

rrn_input = input('Masukkan value RRN (Ref No) \nInput --> ')

#for j in range (len(list_baru)) :
j = 0
found = 0
done = 0
no_terminal_id = 0
while (j < len(list_baru)) & (done == 0) :
    row_convert = []
    row = list_baru[j].split(" ") 
    for i in range(len(row)): 
      if (found == 1) & (len(row_convert) == 6)  & (i == count+4) :
        no_terminal_id = 1
      if row[i] != "":
        row_convert.append(row[i])
        if len(row_convert) == 5 :
          if rrn_input == row_convert[4] :
            found = 1
        if (len(row_convert)) == 6 :
          count = i
      if (found == 1) & (i == len(row) - 1) :
        rrn_row = row_convert
        done = 1
    j += 1

if found == 0 :
  print('\nRRN Not Found on SF')
else :
  if no_terminal_id == 1 :
    row_convert.insert(6,'')

  tanggal = datetime.strptime(rrn_row[2], str(format)) #format tanggal sesuai input
  tanggal = tanggal.strftime('%Y%m%d') #format yyyymmdd
  rrn_row[2] = tanggal

  if (rrn_row[14] == '0') or (rrn_row[14] == '00'):
    status = "SUCCESS"
  elif (rrn_row[14] == '68'):
    status = "MORE"

  rrn_row = [s.replace(":", "") for s in rrn_row]
  value_order = [2, 9, 3, 10, 4]
  rrn_row_ordered = [rrn_row[i] for i in value_order]
  ESN = convert(rrn_row_ordered)


  output_filename = 'History/history_' + str(rrn_input) + '.txt'
  fOutput = open(output_filename, "w")

  fOutput.write('Ref_no : ' + str(rrn_input))
  fOutput.write('\nESN    : ' + str(ESN))
  fOutput.write('\nStatus : ' + str(status))
  fOutput.close()

  print('\nESN  : ' + str(ESN))
  print('Status : ' + str(status))


next = input("\n  --- Press enter to close ---")
