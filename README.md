# landsat_validation_bulk_download

## Overview

This project provides a data downloading service that allows users to request and download data files based on specific parameters. The service consists of two parts:
1. The server-side code processes data requests based on user inputs.
2. The client-side code allows users to interact with the server and download filtered data.

The server generates a data file based on the user's request, and the client downloads this file through an FTP connection after establishing a TCP connection to communicate with the server.

---

## Prerequisites

- **Python 3.10 or higher**: This project requires Python 3.10 or newer to run.
- **Telnet Client (macOS)**: For macOS users who need to use the Telnet client via the command line, you can install it with Homebrew:
   ```bash
   brew install telnet
   ```
All other dependencies, including FTP (`ftplib`), TCP (`socket`), and Telnet (`telnetlib`), are part of Python's standard library and do not require additional installation.
Linux and windows DONT need any kind of installations, as long you have a python version of 3.10 or higher.

---

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/your-repo-name.git
   cd your-repo-name
   ```

2. Ensure that you are using Python 3.10 or higher:
   ```bash
   python --version
   ```

3. The code is now ready to be used for both client-side and server-side operations.

---

## Usage (Client-Side)

To run the client-side code, the user must provide the following parameters:

```bash
usage: python3 client.py [-h] --source {L8,L9} --startdate STARTDATE --enddate ENDDATE [--dd DD] [--distance DISTANCE] [--cloudcover CLOUDCOVER] [--buoyid BUOYID [BUOYID ...]] [--outfile OUTFILE]
```

- **--source**: The data source. Possible values are `L8` (Landsat 8) and `L9` (Landsat 9).
- **--startdate**: The start date for the data retrieval process in the format `YYYY-MM-DD`.
- **--enddate**: The end date for the data retrieval process in the format `YYYY-MM-DD`.
- **--dd**: (Optional) Dewpoint depression value (default: `None`).
- **--distance**: (Optional) Distance to clouds (default: `None`).
- **--cloudcover**: (Optional) The cloud cover percentage filter (default: `None`).
- **--buoyid**: (Optional) One or more Buoy IDs to filter data.
- **--outfile**: (Optional) The name of the output file to save the results. If not provided, a default name will be generated by the server.

### Example Usage

```bash
python client.py --source L8 --startdate 2023-01-01 --enddate 2023-06-30 --cloudcover 20 --buoyid 1234 5678 --outfile output.csv
```

In this example, the user requests data from the `L8` (Landsat 8) source, with a date range from January 1, 2023, to June 30, 2023, filtered by a cloud cover percentage of 20% and data from Buoy IDs `1234` and `5678`. The output will be saved in `output.csv`.

---

## How It Works

1. **Client-Side:**
   - The user downloads the client-side code from GitHub.
   - The user runs the client-side code by specifying parameters such as the data source, date range, and additional filters (like cloud cover, buoy IDs, etc.).
   - The client-side code verifies the user-provided parameters for validity.

2. **Server-Side:**
   - The client establishes a TCP connection with the server and sends over the user-specified parameters.
   - The server processes the request, filters the data accordingly, and generates a file.
   - The server responds to the client with a unique file name for the requested data and terminates the TCP connection.

3. **Data Download:**
   - After receiving the file name from the server, the client establishes an FTP connection with the server.
   - The client downloads the file generated by the server using the provided file name.
   - The FTP connection is then terminated, and the file is saved locally.

---

The server will listen for incoming TCP connections from the client. Once a client connects and sends data parameters, the server will generate a file and handle the FTP connection for file download.
