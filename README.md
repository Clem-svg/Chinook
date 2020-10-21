# README

Niveau Facile

Quel est le nombre total d'objets Album contenus dans la base (sans regarder les id bien sûr) ?
------------------------------------------------------------------------------------------------
Album.count
/home/clementine/.rvm/gems/ruby-2.7.1/gems/activemodel-5.2.4.4/lib/active_model/type/integer.rb:13: warning: Using the last argument as keyword parameters is deprecated; maybe ** should be added to the call
/home/clementine/.rvm/gems/ruby-2.7.1/gems/activemodel-5.2.4.4/lib/active_model/type/value.rb:8: warning: The called method `initialize' is defined here
   (0.1ms)  SELECT COUNT(*) FROM "albums"
 => 347


qui est l'auteur de la chanson "White Room" ?
-----------------------------------------------
2.7.1 :011 > Track.find_by(title: "white Room").artist
  Track Load (0.3ms)  SELECT  "tracks".* FROM "tracks" WHERE "tracks"."title" = ? LIMIT ?  [["title", "white Room"], ["LIMIT", 1]]
Traceback (most recent call last):
        2: from (irb):10
        1: from (irb):11:in `rescue in irb_binding'
NoMethodError (undefined method `artist' for nil:NilClass)
2.7.1 :012 > Track.find_by(title: "White Room").artist
  Track Load (0.3ms)  SELECT  "tracks".* FROM "tracks" WHERE "tracks"."title" = ? LIMIT ?  [["title", "White Room"], ["LIMIT", 1]]
 => "Eric Clapton"



Quelle chanson dure exactement 188133 milliseconds ?
----------------------------------------------------
Track.find_by(duration: 188133).title
  Track Load (0.3ms)  SELECT  "tracks".* FROM "tracks" WHERE "tracks"."duration" = ? LIMIT ?  [["duration", 188133], ["LIMIT", 1]]
 => "Perfect"



Quel groupe a sorti l'album "Use Your Illusion II" ?
-----------------------------------------------------
2.7.1 :014 > Album.find_by(title: "Use Your Illusion II").artist
  Album Load (0.3ms)  SELECT  "albums".* FROM "albums" WHERE "albums"."title" = ? LIMIT ?  [["title", "Use Your Illusion II"], ["LIMIT", 1]]
 => "Guns N Roses"


Niveau Moyen

Combien y a t'il d'albums dont le titre contient "Great" ? (indice)
--------------------------------------------------------------------
Album.where("title like ?", "%Great%").count
13


Supprime tous les albums dont le nom contient "music".
------------------------------------------------------
Album.where("title like ?", "%music%").destroy_all


Combien y a t'il d'albums écrits par AC/DC ?
--------------------------------------------

2.7.1 :019 > Album.where(artist: "AC/DC").count
   (0.2ms)  SELECT COUNT(*) FROM "albums" WHERE "albums"."artist" = ?  [["artist", "AC/DC"]]
 => 2


Combien de chanson durent exactement 158589 millisecondes ?
-----------------------------------------------------------
2.7.1 :021 > Track.where(duration: 158589).count
   (0.4ms)  SELECT COUNT(*) FROM "tracks" WHERE "tracks"."duration" = ?  [["duration", 158589]]
 => 0


Niveau Difficile

puts en console tous les titres de AC/DC.
-----------------------------------------
acdc_songs = Track.where(artist: "AC/DC")

acdc_songs.map {|song| puts song.title}


puts en console tous les titres de l'album "Let There Be Rock".
---------------------------------------------------------------
2.7.1 :031 > Track.where(album: "Let There Be Rock").map {|song| puts song.title}
  Track Load (0.4ms)  SELECT "tracks".* FROM "tracks" WHERE "tracks"."album" = ?  [["album", "Let There Be Rock"]]
Go Down
Dog Eat Dog
Let There Be Rock
Bad Boy Boogie
Problem Child
Overdose
Hell Aint A Bad Place To Be
Whole Lotta Rosie


Calcule le prix total de cet album ainsi que sa durée totale.
-------------------------------------------------------------
2.7.1 :007 > Track.where(album: "Let There Be Rock").sum(:price)
   (0.2ms)  SELECT SUM("tracks"."price") FROM "tracks" WHERE "tracks"."album" = ?  [["album", "Let There Be Rock"]]
 => 7.920000000000001

2.7.1 :008 > Track.where(album: "Let There Be Rock").sum(:duration)
   (0.5ms)  SELECT SUM("tracks"."duration") FROM "tracks" WHERE "tracks"."album" = ?  [["album", "Let There Be Rock"]]
 => 2453259


Calcule le coût de l'intégralité de la discographie de "Deep Purple".
---------------------------------------------------------------------
Track.where(artist: "Deep Purple").sum(:price)

Modifie (via une boucle) tous les titres de "Eric Clapton" afin qu'ils soient affichés avec "Britney Spears" en artist.
-----------------------------------------------------------------------------------------------------------------------

2.7.1 :011 > clapton = Track.where(artist: "Eric Clapton")
2.7.1 :012 > clapton
  Track Load (0.4ms)  SELECT  "tracks".* FROM "tracks" WHERE "tracks"."artist" = ? LIMIT ?  [["arti
 => #<ActiveRecord::Relation [#<Track id: 499, title: "Layla", album: "The Cream Of Clapton", artist: "Eric Clapton", duration: 430733, size: 14115792, price: 0.99, created_at: "2020-10-21 16:42:08", updated_at: "2020-10-21 16:42:08">, #<Track id: 500, title: "Badge", album: "The Cream Of Clapton", artist: "Eric Clapton", duration: 163552, size: 5322942, price: 0.99, created_at: "2020-10-21 16:42:09", updated_at: "2020-10-21 16:42:09">, #<Track id: 501, title: "I Feel Free", album: "The Cream Of Clapton", artist: "Eric Clapton", duration: 174576, size: 5725684, price: 0.99, created_at: "2020-10-21 16:42:09", updated_at: "2020-10-21 16:42:09">, #<Track id: 502, title: "Sunshine Of Your Love", album: "The Cream\n Of Clapton", artist: "Eric Clapton", duration: 252891, size: 8225889, p
 title: "Crossroads", album: "The Cream Of Clapton", artist: "Eric Clapton", duration: 253335, size: 8273540, price: 0.99, created_at: "2020-10-21 16:42:09", updated_at: "2020-10-21 16:42:09">, #<Track id: 504, title: "Strange Brew", album: "The Cream Of Clapton", artist: "Eric Clapton", duration: 167810, size: 5489787, price: 0.99, created_at: "2020-10-21 16:42:09", updated_at: "2020-10-21 16:42:09">, #<Track id: 505, title: "White Room", album: "The Cream Of Clapton", artist: "Eric Clapton", duration: 301583, size: 9872606, price: 0.99, created_at: "2020-10-21 16:42:09", updated_at: "2020-10-21 16:42:09">, #<Track id: 506, title: "Bell Bottom Blues", album: "The Cream Of Clapton", artist: "Eric Clapton", duration: 304744, size: 9946681, price: 0.99, created_at: "2020-10-21 16:42:09", updated_at: "2020-10-21 16:42:09">, #<Track id: 507, title: "Cocaine", album: "The Cream Of Clapton", artist: "Eric Clapton", duration: 215928, size: 7138399, price: 0.99, created_at: "2020-10-21 16:42:09", updated_at: "2020-10-21 16:42:09">, #<Track id: 508, title: "I Shot The Sheriff", album: "The Cream Of Clapton", artist: "Eric Clapton", duration: 263862, size: 8738973, price: 0.99, created_at: "2020-10-21 16:42:09", updated_at: "2020-10-21 16:42:09">, ...]>

2.7.1 :013 > clapton.map{|song|song.artist = "Britney Spears"}
