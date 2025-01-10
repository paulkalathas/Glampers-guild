// Generate a new sequential Trip ID
function generateTripId() {
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName('Trips');
  const lastRow = sheet.getLastRow();
  let newId = 'GGTP_00001';

  if (lastRow > 1) {
    const lastId = sheet.getRange(lastRow, 1).getValue();
    const number = parseInt(lastId.split('_')[1]) + 1;
    newId = 'GGTP_' + number.toString().padStart(5, '0');
  }
  return newId;
}

// Generate a new sequential Booking ID
function generateBookingId() {
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName('Bookings');
  const lastRow = sheet.getLastRow();
  let newId = 'GGBK_00001';

  if (lastRow > 1) {
    const lastId = sheet.getRange(lastRow, 1).getValue();
    const number = parseInt(lastId.split('_')[1]) + 1;
    newId = 'GGBK_' + number.toString().padStart(5, '0');
  }
  return newId;
}

// Web app entry point
function doGet(e) {
  return HtmlService.createHtmlOutputFromFile('index');
}

// Create a new camping trip
function createTrip(tripData) {
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName('Trips');
  const tripId = generateTripId();
  sheet.appendRow([
    tripId,
    tripData.tripName,
    tripData.organizer,
    tripData.startDate,
    tripData.endDate,
    tripData.location
  ]);
  return tripId;
}

// Create a new booking
function createBooking(bookingData) {
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName('Bookings');
  const bookingId = generateBookingId();
  sheet.appendRow([
    bookingId,
    bookingData.tripId,
    bookingData.bookingName,
    bookingData.email,
    bookingData.phone,
    bookingData.adults,
    bookingData.children,
    bookingData.pets,
    bookingData.days
  ]);
  return bookingId;
}

// Retrieve a booking by Booking ID
function getBooking(bookingId) {
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName('Bookings');
  const data = sheet.getDataRange().getValues();
  for (let i = 1; i < data.length; i++) {
    if (data[i][0] === bookingId) {
      return {
        bookingId: data[i][0],
        tripId: data[i][1],
        bookingName: data[i][2],
        email: data[i][3],
        phone: data[i][4],
        adults: data[i][5],
        children: data[i][6],
        pets: data[i][7],
        days: data[i][8]
      };
    }
  }
  return { error: 'Booking not found' };
}

// Update an existing booking
function updateBooking(updatedData) {
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName('Bookings');
  const data = sheet.getDataRange().getValues();
  for (let i = 1; i < data.length; i++) {
    if (data[i][0] === updatedData.bookingId) {
      sheet.getRange(i + 1, 2, 1, 8).setValues([[
        updatedData.tripId,
        updatedData.bookingName,
        updatedData.email,
        updatedData.phone,
        updatedData.adults,
        updatedData.children,
        updatedData.pets,
        updatedData.days
      ]]);
      return 'Booking updated successfully';
    }
  }
  return 'Booking not found';
}