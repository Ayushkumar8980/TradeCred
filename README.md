# TradeCred
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
from numpy import array
import requests


# response = requests.get("/content/test_documents_upload.xls")
# print(response.status_code)      200
# print(response.data)

# tradecred.com/getTotalSumAmount    =     sumOfInvoicesAmount(dataset)

# tradecred.com/numberOfInvoicesUploaded        =   calculateInvoicesUploaded(invoiceColumn)

# tradecred.com/totalVendors      =        otalNumberOfVendors(dataset)

# tradecred.com/invalidInvoices        =        invalidInvoices(invoiceColumn)

dataset = pd.read_excel('test_documents_upload.xls')
allValues=dataset.iloc[:, :].values

invoiceColumn = dataset.iloc[:, :-9].values

def validationToRemoveDuplicates(invoiceColumn):
  for i in range (len(invoiceColumn)):
    # checking invoice is  not 0 or null
    if invoiceColumn[i] != 0 and invoiceColumn[i] != "":
      # checking duplicates
      invoiceColumnwithoutDuplicates = [] 
      for i in invoiceColumn: 
          if i not in invoiceColumnwithoutDuplicates: 
              invoiceColumnwithoutDuplicates.append(i) 
  # list after removing duplicates
  return invoiceColumnwithoutDuplicates

def calculateInvoicesUploaded(invoiceColumn):
  totalInvoicesUploaded = len(invoiceColumn)
  invoiceWithoutDuplicates = validationToRemoveDuplicates(invoiceColumn)
  invoicesUploaded[0] = totalInvoicesUploaded
  invoicesUploaded[1] = invoiceWithoutDuplicates
  # returns total number of invoices uploaded (without duplicates)
  return invoicesUploaded

def sumOfInvoicesAmount(dataset):
  totalSumOfInvoiceAmount = 0
  amountColumn = dataset.iloc[:, 6:-3].values
  for i in amountColumn:
    totalSumOfInvoiceAmount = totalSumOfInvoiceAmount + i
  # returns total sum of Invoice Amounts
  return totalSumOfInvoiceAmount

def totalNumberOfVendors(dataset):
  vendorColumn = dataset.iloc[:, 7:-2]
  numberOfVendors = len(vendorColumn);
  # returns total number of vendors
  return numberOfVendors;

def invalidInvoices(invoiceColumn):
  counter = 0
  for i in range (len(invoiceColumn)):
    # checking duplicates 
    for j in range (len(invoiceColumn)):
      if i != j:
        if invoiceColumn[j] == invoiceColumn[i]:
          print(invoiceColumn[j])
          counter+=1
  # returns number of duplicate rows
  return counter
