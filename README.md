[ER diagram.pdf](https://github.com/user-attachments/files/24151208/ER.diagram.pdf)
[Inlämninguppgift 1 MusicLibrary.sql](https://github.com/user-attachments/files/24151370/Inlamninguppgift.1.MusicLibrary.sql)

-- Switch to your database
--USE [Inl�mningsuppgift MusicLibrary];
--GO


-- Drop tables
--IF OBJECT_ID('Track', 'U') IS NOT NULL DROP TABLE Track;
--IF OBJECT_ID('Album', 'U') IS NOT NULL DROP TABLE Album;
--IF OBJECT_ID('Band', 'U') IS NOT NULL DROP TABLE Band;
--GO

----------------------------------
-- Creating Tables in the database

-- Table to store bands
--  CREATE TABLE Band (
  --  Id INT IDENTITY(1,1) PRIMARY KEY,       -- Primary key
  --  Name NVARCHAR(100) NOT NULL,            -- Band name
  --  Genre NVARCHAR(50),                      -- Genre of music
  --  Country NVARCHAR(50),                    -- Country of origin
  --  YearFormed INT                            -- Year formed
-- );
-- GO

-- Table to store albums
-- CREATE TABLE Album (
   -- Id INT IDENTITY(1,1) PRIMARY KEY,       -- Primary key
   -- BandId INT NOT NULL,                     -- Foreign key to Band
   -- Title NVARCHAR(100) NOT NULL,           -- Album title
   -- ReleaseYear INT,                         -- Year of release
   -- Genre NVARCHAR(50),                      -- Album genre
   -- CONSTRAINT FK_Album_Band FOREIGN KEY (BandId) REFERENCES Band(Id)
--  );
-- GO


-- CREATE TABLE Track (
   --  Id INT IDENTITY(1,1) PRIMARY KEY,       -- Primary key
   -- AlbumId INT NOT NULL,                    -- Foreign key to Album
   -- Title NVARCHAR(100) NOT NULL,           -- Track title
   -- Length TIME,                             -- Track duration
   -- TrackNumber INT,                          -- Track position
   -- CONSTRAINT FK_Track_Album FOREIGN KEY (AlbumId) REFERENCES Album(Id)
-- );
-- GO

------------------------------------

-- Inserting bands and checking that it worked

-- INSERT INTO Band (Name, Genre, Country, YearFormed)
-- VALUES 
   -- ('Iron Hammer', 'Metal', 'Sweden', 2005),
   -- ('Rolling Beats', 'Rock', 'USA', 1998),
   -- ('Rebel Notes', 'Punk', 'UK', 2010);

-- Show all bands in the Band table
-- SELECT * 
-- FROM Band;


-------------------------------------

-- Inserting albums and checking that it worked

-- Check current bands and their Ids
-- SELECT Id, Name FROM Band;

-- Insert 2 albums per band
-- INSERT INTO Album (BandId, Title, ReleaseYear, Genre)
-- VALUES
    -- Iron Hammer (Metal)
    -- (1, 'Steel Fury', 2008, 'Metal'),
    -- (1, 'Hammer of Doom', 2012, 'Metal'),

    -- Rolling Beats (Rock)
    -- (2, 'Rock Revolution', 2000, 'Rock'),
    -- (2, 'Highway Rhythms', 2005, 'Rock'),

    -- Rebel Notes (Punk)
    -- (3, 'Street Rebellion', 2011, 'Punk'),
    -- (3, 'No Rules', 2014, 'Punk');

    -- Show all albums
        --SELECT * FROM Album;

        -----------------------------------

-- Inserting tracks and checking that it worked

   -- Check album IDs
-- SELECT Id, Title, BandId FROM Album;

-- Insert tracks for all albums
--INSERT INTO Track (AlbumId, Title, Length, TrackNumber)
--VALUES
--    -- Album 1: Steel Fury
--    (1, 'Iron Strike', '00:04:20', 1),
--    (1, 'Metal Storm', '00:05:10', 2),
--    (1, 'Nightforge', '00:03:55', 3),

--    -- Album 2: Hammer of Doom
--    (2, 'Doombringer', '00:06:05', 1),
--    (2, 'Fire and Steel', '00:04:45', 2),
--    (2, 'Battle Cry', '00:05:30', 3),

--    -- Album 3: Rock Revolution
--    (3, 'Rebel Heart', '00:03:40', 1),
--    (3, 'High Voltage', '00:04:15', 2),
--    (3, 'Road Kings', '00:05:00', 3),

--    -- Album 4: Highway Rhythms
--    (4, 'Midnight Drive', '00:04:05', 1),
--    (4, 'Rolling Free', '00:03:55', 2),
--    (4, 'Open Road', '00:04:50', 3),

--    -- Album 5: Street Rebellion
--    (5, 'Anarchy Night', '00:03:20', 1),
--    (5, 'Punk Uprising', '00:02:55', 2),
--    (5, 'No Control', '00:03:10', 3),

--    -- Album 6: No Rules
--    (6, 'Chaos Theory', '00:03:45', 1),
--    (6, 'Break the Chains', '00:04:05', 2),
--    (6, 'Final Stand', '00:04:25', 3);

---- Show all tracks, albums and bands in a column
--SELECT t.Id AS TrackId, t.Title AS TrackTitle, t.Length, t.TrackNumber,
--       a.Title AS AlbumTitle, b.Name AS BandName
--FROM Track t
--JOIN Album a ON t.AlbumId = a.Id
--JOIN Band b ON a.BandId = b.Id
--ORDER BY b.Id, a.Id, t.TrackNumber;

-----------------------------------------------------

-- creating a duplicate, then finding the duplicate, in the end deleting the duplicate

-- Insert a duplicate of track with Id = 1
-- INSERT INTO Track (AlbumId, Title, Length, TrackNumber)
-- SELECT AlbumId, Title, Length, TrackNumber
-- FROM Track
-- WHERE Id = 1;

-- Find duplicate tracks
-- SELECT AlbumId, Title, COUNT(*) AS DuplicateCount
-- FROM Track
-- GROUP BY AlbumId, Title
-- HAVING COUNT(*) > 1;

-- Delete duplicates but keep the one with the smallest Id
-- WITH Duplicates AS (
   -- SELECT *,
     --      ROW_NUMBER() OVER (PARTITION BY AlbumId, Title ORDER BY Id ASC) AS rn
    -- FROM Track
-- )
-- DELETE FROM Duplicates
-- WHERE rn > 1;

--------------------------------------------------------------
