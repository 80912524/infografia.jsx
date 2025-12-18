import React, { useState, useMemo } from 'react';
import { 
  TreeDeciduous, 
  Leaf, 
  Droplets, 
  Map, 
  Search, 
  Info, 
  ChevronRight, 
  ArrowUpRight, 
  Wind,
  LayoutDashboard,
  ExternalLink
} from 'lucide-react';

const rawData = [
  {
    nombre: "Av Mutis. Calle 63 desde la Transversal 112 B Bis a la carrera 114",
    contrato: "1397-2017",
    talados: 146,
    trasladados: 8,
    permanencia: 8,
    plantados: 94,
    especiesArboles: "Yarumo, Pino Romerón, Eucalipto Pomarroso",
    zonasVerdesFinal: 1670.31,
    jardineriaM2: 451,
    especiesJardin: "Bella a las 11, Ajo de rico, Clavel chino, Escarcha, Lirio hibrido, Lirio iris, Siete cueros mexicano, Agapanto, Aclepia, Manto Maria, Capuchina, Gazania, Begonia de invierno",
    suds: 0,
    tipologiasSuds: "N.A"
  },
  {
    nombre: "Ciclopuente Av Boyacá por calle 80",
    contrato: "1807-2021",
    talados: 14,
    trasladados: 28,
    permanencia: 5,
    plantados: 55,
    especiesArboles: "Abutilón, Alcaparro doble, Calistemo llorón, Chicalá",
    zonasVerdesFinal: 9334.5,
    jardineriaM2: 9586.77,
    especiesJardin: "Pennisetum sp, Liriope sp y Escarcha o rocío (Aptenia cordifolia), Claveles chinos (Lamprantus spectabilis)",
    suds: 35,
    tipologiasSuds: "Cuneta verde, alcorque inundable"
  },
  {
    nombre: "Corredor Ambiental Canal Cordóba",
    contrato: "1650-2019",
    talados: 198,
    trasladados: 758,
    permanencia: 628,
    plantados: 628,
    especiesArboles: "Abutilón, Chilco, Cariseco, Tinto, Gaque, Fucsia arbustiva, Fucsia boliviana, Arrayán, Mano de oso, Pino romerón, Mermelada, Garrocho, Hayuelo, Guamo, Magnolio, Siete Cueros, Raque",
    zonasVerdesFinal: 85693,
    jardineriaM2: 666,
    especiesJardin: "Dietes, Pennisetum sp, salvia leucantha",
    suds: 11,
    tipologiasSuds: "Alcorque inundable"
  },
  {
    nombre: "Extensión Av Boyacá entre calle 170 y 183",
    contrato: "1777-2021",
    talados: 142,
    trasladados: 51,
    permanencia: 0,
    plantados: 154,
    especiesArboles: "N.A",
    zonasVerdesFinal: 22021.21,
    jardineriaM2: 969422,
    especiesJardin: "Hiedra miami, Pennisetum sp.",
    suds: 0,
    tipologiasSuds: "N.A"
  },
  {
    nombre: "Refuerzo puentes vehículares grupo 2",
    contrato: "1826-2021",
    talados: 47,
    trasladados: 4,
    permanencia: 65,
    plantados: 3,
    especiesArboles: "Arrayán",
    zonasVerdesFinal: 0,
    jardineriaM2: 0,
    especiesJardin: "N.A",
    suds: 0,
    tipologiasSuds: "N.A"
  },
  {
    nombre: "Patio la Reforma",
    contrato: "1712-2020",
    talados: 36,
    trasladados: 45,
    permanencia: 12,
    plantados: 182,
    especiesArboles: "Alcaparro, Arbol loco, Arrayan, Cajeto, Chicala amarillo, Corono, Espino de hoja pequeña, Garrocho, Gaque, Hayuelo, Laurel de cera",
    zonasVerdesFinal: 4321,
    jardineriaM2: 240,
    especiesJardin: "Azahar de la china, Eugenia, Pasto kikuyo",
    suds: 2,
    tipologiasSuds: "Zanja de infiltración"
  },
  {
    nombre: "Av. Laureano Gómez (Av Cra 9) de la calle 170 a la calle 193",
    contrato: "1548-2018",
    talados: 512,
    trasladados: 88,
    permanencia: 34,
    plantados: 742,
    especiesArboles: "Sauce llorón, Siete cueros, Caucho sabanero, Arrayán, Cerezo, Chicalá rosa",
    zonasVerdesFinal: 35400,
    jardineriaM2: 12500,
    especiesJardin: "Agapanto, Lirio, Margarita, Salvia, Pennisetum",
    suds: 18,
    tipologiasSuds: "Alcorques inundables, cunetas verdes"
  },
  {
    nombre: "Av. El Rincón desde la Av. Boyacá hasta la Cra 91",
    contrato: "1551-2018",
    talados: 234,
    trasladados: 112,
    permanencia: 45,
    plantados: 456,
    especiesArboles: "Roble, Guayacán de Manizales, Palma de cera, Carbonero",
    zonasVerdesFinal: 18900,
    jardineriaM2: 4200,
    especiesJardin: "Duranta, Azalea, Eugenia, Jazmín",
    suds: 10,
    tipologiasSuds: "Zanjas de infiltración"
  },
  {
    nombre: "Av. 68 Alimentadora Metro - Grupo 1",
    contrato: "1560-2020",
    talados: 89,
    trasladados: 24,
    permanencia: 156,
    plantados: 312,
    especiesArboles: "Jazmín del cabo, San Joaquín, Sangre de Drago, Guayacán",
    zonasVerdesFinal: 12450,
    jardineriaM2: 1800,
    especiesJardin: "Cintas, Siete cueros rastrero, Helechos",
    suds: 5,
    tipologiasSuds: "Alcorques inundables"
  },
  {
    nombre: "Aceras y Ciclorrutas de la Calle 116",
    contrato: "1435-2017",
    talados: 12,
    trasladados: 5,
    permanencia: 240,
    plantados: 88,
    especiesArboles: "Acacia japonesa, Palma fénix, Eucalipto pomarroso",
    zonasVerdesFinal: 15600,
    jardineriaM2: 3200,
    especiesJardin: "Lirio iris, Mora de la india, Barba de dragón",
    suds: 0,
    tipologiasSuds: "N.A"
  },
  {
    nombre: "Espacio Público Zona Rosa",
    contrato: "1357-2017",
    talados: 8,
    trasladados: 2,
    permanencia: 115,
    plantados: 42,
    especiesArboles: "Palma de cera, Magnolia, Siete cueros",
    zonasVerdesFinal: 2100,
    jardineriaM2: 950,
    especiesJardin: "Agapanto, Clavel chino, Duranta mini",
    suds: 4,
    tipologiasSuds: "Alcorques inundables"
  }
];

const StatCard = ({ icon: Icon, label, value, color, unit = "" }) => (
  <div className="bg-white p-4 rounded-2xl shadow-sm border border-slate-100 flex items-center space-x-4">
    <div className={`p-3 rounded-xl ${color}`}>
      <Icon className="w-6 h-6 text-white" />
    </div>
    <div className="overflow-hidden">
      <p className="text-xs text-slate-500 font-medium truncate uppercase tracking-tight">{label}</p>
      <p className="text-xl font-bold text-slate-800">
        {typeof value === 'number' ? value.toLocaleString() : value} 
        <span className="text-xs ml-1 font-normal text-slate-400">{unit}</span>
      </p>
    </div>
  </div>
);

const SectionTitle = ({ title, icon: Icon }) => (
  <div className="flex items-center space-x-2 mb-4 mt-8">
    <Icon className="w-5 h-5 text-emerald-600" />
    <h3 className="text-lg font-bold text-slate-800 uppercase tracking-wider">{title}</h3>
  </div>
);

const Badge = ({ children }) => (
  <span className="px-3 py-1 bg-emerald-50 text-emerald-700 rounded-full text-[10px] font-bold border border-emerald-100 mb-2 mr-2 inline-block shadow-sm">
    {children}
  </span>
);

export default function App() {
  const [selectedIdx, setSelectedIdx] = useState(0);
  const [searchTerm, setSearchTerm] = useState("");

  const filteredProjects = useMemo(() => {
    return rawData.filter(p => 
      p.nombre.toLowerCase().includes(searchTerm.toLowerCase()) || 
      p.contrato.toLowerCase().includes(searchTerm.toLowerCase())
    );
  }, [searchTerm]);

  const p = filteredProjects[selectedIdx] || rawData[0];

  return (
    <div className="min-h-screen bg-slate-50 font-sans text-slate-900">
      {/* Navbar / Header */}
      <header className="bg-emerald-900 text-white p-6 sticky top-0 z-10 shadow-lg border-b border-emerald-800">
        <div className="max-w-6xl mx-auto flex flex-col md:flex-row md:items-center justify-between gap-4">
          <div className="flex items-center space-x-4">
            <div className="bg-emerald-500 p-2 rounded-lg">
              <LayoutDashboard className="w-7 h-7 text-white" />
            </div>
            <div>
              <h1 className="text-xl font-black uppercase tracking-tighter">Impacto Ambiental IDU</h1>
              <p className="text-[10px] text-emerald-300 font-bold uppercase tracking-[0.2em]">Consolidado 11 Proyectos - Nov 2025</p>
            </div>
          </div>
          
          <div className="relative group">
            <Search className="absolute left-3 top-1/2 -translate-y-1/2 w-4 h-4 text-emerald-300 opacity-60 group-focus-within:opacity-100" />
            <input 
              type="text" 
              placeholder="Buscar proyecto o contrato..."
              className="bg-emerald-800/40 border border-emerald-700 text-white placeholder-emerald-400/60 rounded-full py-2 pl-10 pr-4 w-full md:w-80 focus:outline-none focus:ring-2 focus:ring-emerald-400 transition-all text-sm"
              value={searchTerm}
              onChange={(e) => {
                setSearchTerm(e.target.value);
                setSelectedIdx(0);
              }}
            />
          </div>
        </div>
      </header>

      <main className="max-w-6xl mx-auto p-4 md:p-8 grid grid-cols-1 lg:grid-cols-12 gap-8">
        
        {/* Sidebar Project List */}
        <aside className="lg:col-span-4 space-y-3 order-2 lg:order-1">
          <div className="flex items-center justify-between px-2 mb-4">
            <h2 className="text-xs font-black text-slate-400 uppercase tracking-widest">Proyectos en Ejecución</h2>
            <span className="bg-slate-200 text-slate-600 px-2 py-0.5 rounded text-[10px] font-bold">{filteredProjects.length}</span>
          </div>
          <div className="max-h-[75vh] overflow-y-auto space-y-2 pr-2 scrollbar-thin scrollbar-thumb-slate-200">
            {filteredProjects.map((project, idx) => (
              <button
                key={project.contrato}
                onClick={() => setSelectedIdx(idx)}
                className={`w-full text-left p-4 rounded-2xl transition-all duration-300 group border ${
                  selectedIdx === idx 
                    ? 'bg-white border-emerald-500 shadow-md ring-1 ring-emerald-500/20 translate-x-2' 
                    : 'bg-white/50 border-slate-100 hover:bg-white hover:border-slate-300'
                }`}
              >
                <div className="flex items-start justify-between">
                  <div className="flex-1">
                    <div className="flex items-center gap-2 mb-1">
                      <span className={`text-[9px] font-black px-1.5 py-0.5 rounded ${selectedIdx === idx ? 'bg-emerald-100 text-emerald-700' : 'bg-slate-100 text-slate-500'}`}>
                        ID: {project.contrato}
                      </span>
                    </div>
                    <h4 className={`text-xs font-bold leading-relaxed ${selectedIdx === idx ? 'text-slate-900' : 'text-slate-600'}`}>
                      {project.nombre}
                    </h4>
                  </div>
                  <ChevronRight className={`w-4 h-4 mt-1 shrink-0 transition-transform ${selectedIdx === idx ? 'text-emerald-500 translate-x-1' : 'text-slate-300'}`} />
                </div>
              </button>
            ))}
          </div>
        </aside>

        {/* Main Content Area / Infographic */}
        <div className="lg:col-span-8 order-1 lg:order-2">
          {filteredProjects.length > 0 ? (
            <div className="bg-white rounded-[2rem] shadow-2xl shadow-slate-200/50 overflow-hidden border border-slate-100">
              {/* Project Hero */}
              <div className="bg-gradient-to-br from-emerald-600 via-emerald-700 to-emerald-900 p-8 md:p-10 relative">
                <div className="absolute top-0 right-0 w-64 h-64 bg-white/5 rounded-full -mr-20 -mt-20 blur-3xl"></div>
                <div className="relative z-10">
                  <div className="flex flex-wrap items-center gap-3 mb-6">
                    <div className="flex items-center space-x-2 bg-white/10 backdrop-blur-md text-white px-4 py-1.5 rounded-full text-[10px] font-black uppercase tracking-widest border border-white/20">
                      <Map className="w-3 h-3" />
                      <span>Ficha Ambiental</span>
                    </div>
                    <span className="text-emerald-300 text-[10px] font-mono font-bold tracking-widest bg-black/20 px-3 py-1.5 rounded-full border border-white/5">
                      OBRA: {p.contrato}
                    </span>
                  </div>
                  <h2 className="text-2xl md:text-4xl font-black text-white leading-[1.1] mb-2">
                    {p.nombre}
                  </h2>
                </div>
              </div>

              <div className="p-6 md:p-10">
                {/* Stat Grid */}
                <div className="grid grid-cols-2 md:grid-cols-4 gap-4 -mt-16 md:-mt-20 relative z-20 mb-10">
                  <StatCard icon={TreeDeciduous} label="Plantados" value={p.plantados} color="bg-emerald-500" />
                  <StatCard icon={Wind} label="Talados" value={p.talados} color="bg-rose-500" />
                  <StatCard icon={Leaf} label="Verde Final" value={p.zonasVerdesFinal} color="bg-teal-500" unit="m²" />
                  <StatCard icon={Droplets} label="SUDS" value={p.suds} color="bg-blue-500" />
                </div>

                <div className="grid grid-cols-1 md:grid-cols-2 gap-10">
                  
                  {/* Column 1: Vegetation */}
                  <div className="space-y-6">
                    <SectionTitle title="Manejo Silvicultural" icon={TreeDeciduous} />
                    
                    <div className="bg-slate-50 p-6 rounded-3xl border border-slate-100 group hover:border-emerald-200 transition-colors">
                      <div className="flex justify-between items-center mb-4">
                        <span className="text-[11px] font-black text-slate-400 uppercase tracking-widest">Diversidad de Especies</span>
                        <div className="bg-emerald-100 p-1.5 rounded-full">
                          <ExternalLink className="w-3 h-3 text-emerald-600" />
                        </div>
                      </div>
                      <div className="flex flex-wrap gap-1">
                        {p.especiesArboles === "N.A" ? (
                          <span className="text-sm italic text-slate-400">Sin especies forestales registradas</span>
                        ) : (
                          p.especiesArboles.split(',').map((esp, i) => (
                            <Badge key={i}>{esp.trim()}</Badge>
                          ))
                        )}
                      </div>
                    </div>

                    <div className="grid grid-cols-2 gap-4">
                      <div className="bg-slate-50 p-5 rounded-3xl border border-slate-100">
                        <p className="text-[10px] text-slate-400 font-bold uppercase mb-1">Traslados</p>
                        <p className="text-2xl font-black text-slate-800">{p.trasladados}</p>
                      </div>
                      <div className="bg-slate-50 p-5 rounded-3xl border border-slate-100">
                        <p className="text-[10px] text-slate-400 font-bold uppercase mb-1">Permanencia</p>
                        <p className="text-2xl font-black text-slate-800">{p.permanencia}</p>
                      </div>
                    </div>
                  </div>

                  {/* Column 2: Gardening & SUDS */}
                  <div className="space-y-6">
                    <SectionTitle title="Paisajismo y Drenaje" icon={Leaf} />
                    
                    <div className="bg-emerald-50/50 p-6 rounded-3xl border border-emerald-100">
                      <div className="flex justify-between items-center mb-3">
                        <span className="text-[11px] font-black text-emerald-700 uppercase tracking-widest">Jardinería Plantada</span>
                        <span className="text-2xl font-black text-emerald-600">{p.jardineriaM2.toLocaleString()} <span className="text-xs font-normal">m²</span></span>
                      </div>
                      <div className="border-t border-emerald-100 pt-4">
                        <div className="flex flex-wrap">
                          {p.especiesJardin === "N.A" ? (
                            <span className="text-xs italic text-emerald-600/60">No aplica</span>
                          ) : (
                            p.especiesJardin.split(',').map((esp, i) => (
                              <span key={i} className="text-[10px] text-emerald-800 bg-white px-2 py-1 rounded-md mr-2 mb-2 shadow-sm border border-emerald-100">
                                {esp.trim()}
                              </span>
                            ))
                          )}
                        </div>
                      </div>
                    </div>

                    <div className={`p-6 rounded-3xl border transition-all duration-300 ${p.suds > 0 ? 'bg-blue-50 border-blue-100' : 'bg-slate-50 border-slate-100 opacity-60'}`}>
                      <div className="flex items-center space-x-3 mb-3">
                        <div className={`p-2 rounded-xl ${p.suds > 0 ? 'bg-blue-500' : 'bg-slate-300'}`}>
                          <Droplets className="w-4 h-4 text-white" />
                        </div>
                        <span className={`text-[11px] font-black uppercase tracking-widest ${p.suds > 0 ? 'text-blue-700' : 'text-slate-500'}`}>Sistemas SUDS</span>
                      </div>
                      {p.suds > 0 ? (
                        <div>
                          <p className="text-3xl font-black text-blue-800">{p.suds} <span className="text-sm font-normal">Sistemas</span></p>
                          <div className="mt-3 flex items-start gap-2 bg-white/50 p-3 rounded-xl border border-blue-200">
                            <Info className="w-4 h-4 text-blue-400 shrink-0 mt-0.5" />
                            <p className="text-[11px] text-blue-900 leading-relaxed italic">
                              <span className="font-bold">Tipologías:</span> {p.tipologiasSuds}
                            </p>
                          </div>
                        </div>
                      ) : (
                        <p className="text-xs text-slate-400 font-medium">No se registran sistemas de drenaje sostenible.</p>
                      )}
                    </div>
                  </div>
                </div>

                {/* Legend / Info */}
                <div className="mt-12 bg-slate-900 rounded-2xl p-6 flex flex-col md:flex-row items-center justify-between gap-6 overflow-hidden relative">
                  <div className="absolute top-0 right-0 w-32 h-full bg-emerald-500 skew-x-12 translate-x-16 opacity-10"></div>
                  <div className="flex items-center space-x-4 relative z-10">
                    <div className="bg-slate-800 p-3 rounded-full border border-slate-700">
                      <Info className="w-5 h-5 text-emerald-400" />
                    </div>
                    <div>
                      <p className="text-white text-sm font-bold">Datos Oficiales IDU</p>
                      <p className="text-slate-400 text-xs">Corte de información: Noviembre 2025</p>
                    </div>
                  </div>
                  <div className="text-right relative z-10">
                    <p className="text-slate-500 text-[10px] font-bold uppercase tracking-widest mb-1">Total Plantación Acumulada</p>
                    <p className="text-emerald-400 text-xl font-black">{rawData.reduce((acc, curr) => acc + curr.plantados, 0).toLocaleString()} Árboles</p>
                  </div>
                </div>
              </div>
            </div>
          ) : (
            <div className="bg-white rounded-[2rem] p-20 text-center border-2 border-dashed border-slate-200">
              <div className="bg-slate-100 w-16 h-16 rounded-full flex items-center justify-center mx-auto mb-6">
                <Search className="w-8 h-8 text-slate-300" />
              </div>
              <h3 className="text-xl font-bold text-slate-800 mb-2">No se encontraron proyectos</h3>
              <p className="text-slate-500 max-w-xs mx-auto text-sm">Prueba ajustando el término de búsqueda o revisando el número de contrato.</p>
              <button 
                onClick={() => setSearchTerm("")}
                className="mt-6 text-emerald-600 font-bold text-sm underline underline-offset-4"
              >
                Ver todos los proyectos
              </button>
            </div>
          )}
        </div>
      </main>

      <footer className="max-w-6xl mx-auto p-8 text-center text-slate-400 text-[10px] font-bold uppercase tracking-[0.3em]">
        Instituto de Desarrollo Urbano - Reporte de Sostenibilidad 2025
      </footer>
    </div>
  );
}
