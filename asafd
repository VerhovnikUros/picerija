 using System;
using System.Collections.Generic;
using System.Linq;
using System.IO;
using System.Xml.Serialization;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApp26
{
    public interface IPicerija
    {
        double oddajNaročilo(int id, Naročilo naročilo);
        List<Pica> isciPice(TipPice tip);
        List<Pica> isciPice(double cena);

    }
    public interface INaročilo
    {
        double izračunajCeno();
    }
    public enum TipPice
    {
        vegi,
        mesna

    }
    public class Picerija: IPicerija
    {
        public Dictionary<int, Naročilo> seznamNaročil = new Dictionary<int, Naročilo>();
        private List<Pica> stalnaPonudba;
        private string naziv;
        private string naslov;

        public List<Pica> stalna
        {
            get { return stalnaPonudba; }
            set { stalnaPonudba = value; }
        }
        public string _naziv
        {
            get { return naziv; }
            set { naziv = value; }
        }
        public string _naslov
        {
            get { return naslov; }
            set { naslov = value; }
        }
        public Picerija() { }
        public Picerija(string _naziv,string _naslov)
        {
            this._naziv = _naziv;
            this._naslov = _naslov;
        }

        public Picerija(string _naziv, string _naslov, List<Pica> stalna ):this (_naziv,_naslov)

        {
            this.stalna = stalna;
        }
        public double oddajNaročilo(int id, Naročilo naročilo)
        {
             
            if (naročilo._id == 0 || naročilo.naslov == "" || naročilo.seznam == null || naročilo.datum == null)
            {
                throw new Exception();
            }
            else
            {
                seznamNaročil.Add(id, naročilo);
                double d = naročilo.izračunajCeno();

                return d;
            }
        }
  
        public List<Pica> isciPice(double cena)
        {
           List<Pica>iskanaC= stalna.FindAll(c => c._cena <= cena);
            return iskanaC;

        }
        public List<Pica> isciPice(TipPice tip)
        {
            List<Pica> iskanaT = stalna.FindAll(c => c._tip == tip);
            return iskanaT;
        }
        public Pica picaDneva (List<Pica> list)
        {
            int i = list.Count;
            Random r = new Random();
            int s = r.Next(i);
            return list[s];      
        }
    }
    public class Naročilo:INaročilo
    {
        private int id;
        private DateTime datumNaročila;
        private string naslovDostave;
        private List<Pica> seznamPic;

        public int _id
        {
            get { return id; }
            set { id = value; }
        }
        public DateTime datum
        {
            get { return datumNaročila; }
            set { datumNaročila = value; }
        }
        public string naslov
        {
            get { return naslovDostave; }
            set { naslovDostave = value; }
        }
        public List<Pica>seznam
        {
            get { return seznamPic; }
            set { seznamPic = value; }
        }
        public Naročilo() { }
        public Naročilo(int _id, string naslov)
        {
            this._id = _id;
            this.naslov = naslov;
        }
        public Naročilo(int _id, string naslov, DateTime datum, List<Pica>seznam):this(_id,naslov)
        {
            this.datum = datum;
            this.seznam=seznam;
        }
        public double izračunajCeno( )
        {
            double d = 0;
            foreach (var i in  seznam)
            {
                d = i._cena + d;
            }
            return d;
        }
    }
    public class Pica
    {
        private string naziv;
        private string opisSestavin;
        private TipPice tip;
        private double cena;

        public string _naziv
        {
            get { return naziv; }
            set { naziv = value; }
        }
        public string opis
        {
            get { return opisSestavin; }
            set { opisSestavin = value; }
        }
        public TipPice _tip
        {
            get { return tip; }
            set { tip = value; }
        }
        public double _cena
        {
            get { return cena; }
            set { cena = value; }
        }
        public Pica() { }
        public Pica(string _naziv, string opis)
        {
            this._naziv = _naziv;
            this.opis=opis;
        }
        public Pica(string _naziv, string opis,TipPice _tip,double _cena ):this (_naziv, opis)
        {
            this._tip = _tip;
            this._cena = _cena;
        }

    }
    class Program
    {
        static void Main(string[] args)
        {
            Picerija padrino = new Picerija("Padrino", "bolfenkova 12");

            Pica prva = new Pica("margerita", "sir;mezga");
            prva = new Pica("margarita", "mezga;sir", TipPice.vegi, 5.20);
            Pica druga = new Pica("klasika", "mezga;sir;šunka", TipPice.mesna, 5.90);
            Pica tretja = new Pica("gobanka", "mezga;sir;šunka;gobice", TipPice.mesna, 6.20);
            Pica četrta = new Pica("zelenjavna", "mezga;sir;zelenjava", TipPice.vegi, 5.70);
            Pica peta  = new Pica("sirna", "mezga;sir;sir;sir", TipPice.vegi, 6.20);

            List<Pica> stalnaPadrino = new List<Pica>();
            stalnaPadrino.AddRange(new List<Pica> { prva, druga, tretja, četrta, peta });
            padrino = new Picerija("Padrino", "bolfenkova 12",stalnaPadrino);

            foreach (var i in padrino.stalna)
                Console.WriteLine("stalna ponudba : "+i._naziv+"\n"+i.opis+"\n"+i._tip+"\n"+i._cena+"$\n");

            List<Pica> naročenePice = new List<Pica>();
            naročenePice.AddRange(new List<Pica> { prva, tretja, peta });
            List<Pica> naročenePice1 = new List<Pica>();
            naročenePice1.AddRange(new List<Pica> { prva, tretja, četrta });
            Naročilo prvo = new Naročilo(1, "", new DateTime(2018, 08, 22), naročenePice);
            Naročilo drugo = new Naročilo(2, "rizra 3", new DateTime(2018, 08, 22), naročenePice1);

            try
            {
                double w = padrino.oddajNaročilo(2,drugo);
                Console.WriteLine("Naročilo oddano \n cena naročila: "+ w);
                double d = padrino.oddajNaročilo(1, prvo);
                Console.WriteLine("Naročilo oddano \n cena naročila: " + d);
               
            }
            catch(Exception e)
            {
                Console.WriteLine("nepopolno",e);
            }
            Console.WriteLine();
            List<Pica> najdenaCena= padrino.isciPice(6.1);
            foreach (var i in najdenaCena)
                Console.WriteLine("iskana pica:"+i._naziv);
            List<Pica> najdenaTip = padrino.isciPice(TipPice.mesna);
            foreach (var i in najdenaTip)
                Console.WriteLine("iskana pica:" + i._naziv);
            Console.WriteLine();
            Pica p= padrino.picaDneva(stalnaPadrino);
            Console.WriteLine("pica dneva: "+p._naziv+"\n"+p.opis +"\n"+p._tip+"\n" +p._cena);
            Console.WriteLine();
            Console.WriteLine("cena naročila: "+ prvo.izračunajCeno());
          


            StreamWriter tekst;
            tekst = File.CreateText(@"izhod.txt");
            foreach (var v in najdenaCena)
                tekst.WriteLine("iskana pica:" + v._naziv);
            foreach (var i in najdenaTip)
                tekst.WriteLine("iskana pica:" + i._naziv);
            tekst.WriteLine("pica dneva: " + p._naziv + "\n" + p.opis + "\n" + p._tip + "\n" + p._cena);
            tekst.WriteLine("cena naročila: " + prvo.izračunajCeno());

            tekst.Close();

            Stream stream = File.OpenWrite(Environment.CurrentDirectory + "\\bla.txt");
            XmlSerializer xml = new XmlSerializer(typeof(List<Pica>));
            xml.Serialize(stream, stalnaPadrino);
            stream.Close();




            Console.ReadKey();

        }
    }
}
