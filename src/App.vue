<script setup lang="ts">
import { ref } from 'vue'
import { 
  FileText, 
  User, 
  ClipboardCheck, 
  ArrowRightLeft, 
  Search, 
  Printer, 
  Download,
  Fingerprint,
  CheckCircle2,
  Check
} from 'lucide-vue-next'

const formData = ref({
  expediente: '',
  prcc: '',
  despachoInstruye: '',
  organismoInvestiga: '',
  despachoCustodia: '',
  organismoCustodia: '',
  direccionObtencion: '',
  fechaHora: new Date().toLocaleString(),
})

const obtencion = ref<Record<string, boolean>>({
  '1': false,
  '2': false,
  '3': false,
  '4': false,
})

const motivos = ref<Record<string, boolean>>({
  'Traslado': false,
  'Peritaje': false,
  'Resguardo': false,
  'Disposición Judicial': false,
  'Disposición Final': false,
})

const toggleObtencion = (id: string) => {
  obtencion.value[id] = !obtencion.value[id]
}

const toggleMotivo = (id: string) => {
  motivos.value[id] = !motivos.value[id]
}

const printDoc = () => {
  window.print()
}
</script>

<template>
  <div class="min-h-screen bg-win95-bg pt-4 pb-8 px-4 sm:px-6 lg:px-8 print:p-0 print:bg-white flex flex-col items-center gap-8 text-win95-text font-win95">
    
    <!-- MAIN WINDOW -->
    <div class="w-full max-w-[800px] win95-window flex flex-col print:shadow-none print:border-none print:max-w-none print:w-full print:p-0 print:m-0 print:bg-white">
      
      <!-- Window Title Bar -->
      <div class="win95-titlebar mb-[2px] no-print">
        <div class="flex items-center gap-1.5 overflow-hidden">
          <FileText :size="14" />
          <span class="truncate">PRCC Digital - Registro de Cadena de Custodia</span>
        </div>
        <div class="flex gap-1 shrink-0">
          <button class="win95-button !px-1 !py-0 w-4 h-4 flex items-center justify-center font-bold text-[10px]">_</button>
          <button class="win95-button !px-1 !py-0 w-4 h-4 flex items-center justify-center font-bold text-[10px]">□</button>
          <button class="win95-button !px-1 !py-0 w-4 h-4 flex items-center justify-center font-bold text-[10px]">X</button>
        </div>
      </div>

      <!-- Menu bar -->
      <div class="flex px-1 gap-4 mb-2 text-[11px] border-b border-win95-border-mid pb-1 no-print">
        <span class="cursor-default hover:bg-win95-title-bg hover:text-white px-1"><u>A</u>rchivo</span>
        <span class="cursor-default hover:bg-win95-title-bg hover:text-white px-1"><u>E</u>dición</span>
        <span class="cursor-default hover:bg-win95-title-bg hover:text-white px-1"><u>V</u>er</span>
        <span class="cursor-default hover:bg-win95-title-bg hover:text-white px-1"><u>A</u>yuda</span>
      </div>

      <!-- Header Content -->
      <div class="p-4 flex flex-col gap-4 print:p-0">
        <div class="win95-inset p-4 bg-white flex flex-col sm:flex-row items-center justify-between gap-4 print:border-none print:shadow-none">
          <div class="flex items-center">
            <img src="https://ik.imagekit.io/p5pirzkod/sha256.us/Logo.svg" alt="Logo" class="h-10 object-contain grayscale" />
          </div>
          <div class="text-right">
            <h1 class="text-lg font-bold text-win95-title-bg leading-tight">Planilla de Registro de Cadena de Custodia</h1>
            <p class="text-xs italic">(PRCC) - Sistema de Gestión de Evidencias</p>
          </div>
        </div>

        <!-- Section I: Datos Generales -->
        <fieldset class="win95-outset p-4 mt-2">
          <legend class="px-2 font-bold bg-win95-bg">I. DATOS GENERALES</legend>
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-x-6 gap-y-3">
            <div class="flex flex-col gap-1">
              <label class="text-[11px] font-bold">a. N° de Expediente:</label>
              <input type="text" v-model="formData.expediente" class="win95-input w-full" />
            </div>
            <div class="flex flex-col gap-1">
              <label class="text-[11px] font-bold">b. N° PRCC:</label>
              <input type="text" v-model="formData.prcc" class="win95-input w-full" />
            </div>
            <div class="flex flex-col gap-1 sm:col-span-2">
              <label class="text-[11px] font-bold">c. Despacho que instruye:</label>
              <input type="text" v-model="formData.despachoInstruye" class="win95-input w-full" />
            </div>
            <div class="flex flex-col gap-1 sm:col-span-2">
              <label class="text-[11px] font-bold">d. Organismo que investiga e instructivo:</label>
              <input type="text" v-model="formData.organismoInvestiga" class="win95-input w-full" />
            </div>
            <div class="flex flex-col gap-1 sm:col-span-2">
              <label class="text-[11px] font-bold">e. Despacho que inicia la custodia:</label>
              <input type="text" v-model="formData.despachoCustodia" class="win95-input w-full" />
            </div>
            <div class="flex flex-col gap-1 sm:col-span-2">
              <label class="text-[11px] font-bold">f. Organismo que custodia:</label>
              <input type="text" v-model="formData.organismoCustodia" class="win95-input w-full" />
            </div>
            <div class="flex flex-col gap-1 sm:col-span-2">
              <label class="text-[11px] font-bold">g. Dirección de Obtención:</label>
              <input type="text" v-model="formData.direccionObtencion" class="win95-input w-full" />
            </div>
            <div class="flex flex-col gap-1 sm:col-span-2">
              <label class="text-[11px] font-bold">h. Fecha y Hora:</label>
              <input type="text" v-model="formData.fechaHora" class="win95-input w-full" />
            </div>
          </div>
        </fieldset>

        <!-- Section II: Formas de Obtención -->
        <fieldset class="win95-outset p-4 mt-4">
          <legend class="px-2 font-bold bg-win95-bg">II. FORMAS DE OBTENCIÓN</legend>
          <div class="grid grid-cols-2 sm:grid-cols-4 gap-4">
            <div v-for="(label, num) in {'1': 'Técnica', '2': 'Aseguramiento', '3': 'Consignación', '4': 'Derivación'}" :key="num" 
                 @click="toggleObtencion(num)"
                 class="flex items-center gap-2 cursor-pointer select-none">
              <div :class="['w-4 h-4 win95-inset flex items-center justify-center', obtencion[num] ? 'bg-white' : 'bg-win95-highlight']">
                <div v-if="obtencion[num]" class="w-2 h-2 bg-black"></div>
              </div>
              <span class="text-[11px] font-bold">{{num}}. {{label}}</span>
            </div>
          </div>
        </fieldset>

        <!-- Section III: Funcionario -->
        <fieldset class="win95-outset p-4 mt-6">
          <legend class="px-2 font-bold bg-win95-bg">III. FUNCIONARIO QUE OBTIENE</legend>
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
            <div v-for="title in ['PROTECCIÓN', 'OBSERVACIÓN PRELIMINAR', 'FIJACIÓN', 'COLECCIÓN']" :key="title" class="win95-inset bg-win95-bg p-3">
              <h4 class="text-[11px] font-bold bg-win95-title-bg text-white px-2 mb-3">{{title}}</h4>
              <div class="space-y-3 mb-4">
                <div class="flex flex-col gap-1">
                  <span class="text-[10px] font-bold">a. Nombres y Apellidos:</span>
                  <input type="text" class="win95-input w-full" />
                </div>
                <div class="flex flex-col gap-1">
                  <span class="text-[10px] font-bold">b. C.I:</span>
                  <input type="text" class="win95-input w-full" />
                </div>
              </div>
              <div class="grid grid-cols-3 gap-2">
                <div class="space-y-1">
                  <div class="aspect-square bg-white win95-inset relative flex items-center justify-center">
                    <span class="text-[8px] text-win95-title-bg opacity-30 font-bold absolute top-1 left-1 italic">SIGNATURE</span>
                  </div>
                  <span class="block text-[9px] text-center uppercase">Firma</span>
                </div>
                <div class="space-y-1">
                  <div class="aspect-square bg-white win95-inset relative flex items-center justify-center">
                     <Fingerprint :size="16" class="opacity-10" />
                  </div>
                  <span class="block text-[9px] text-center uppercase leading-tight">Pulgar Izq.</span>
                </div>
                <div class="space-y-1">
                  <div class="aspect-square bg-white win95-inset relative flex items-center justify-center">
                     <Fingerprint :size="16" class="opacity-10" />
                  </div>
                  <span class="block text-[9px] text-center uppercase leading-tight">Pulgar Der.</span>
                </div>
              </div>
            </div>
          </div>
        </fieldset>

        <!-- Section VI: Descripción -->
        <fieldset class="win95-outset p-4 mt-6">
          <legend class="px-2 font-bold bg-win95-bg">VI. DESCRIPCIÓN DE LA EVIDENCIA</legend>
          <div class="win95-inset bg-white overflow-hidden">
            <div v-for="num in 7" :key="num" class="flex items-center px-3 py-1 border-b border-win95-highlight last:border-0 hover:bg-win95-highlight">
              <span class="text-[11px] font-bold text-win95-border-mid w-6">{{num}}</span>
              <input type="text" class="flex-1 bg-transparent border-none focus:ring-0 text-[11px] py-1" placeholder="Ingrese descripción..." />
            </div>
          </div>
          <div class="mt-2 flex items-center justify-between">
            <span class="text-[10px] italic font-bold">Documento: ANEXO A</span>
            <button class="win95-button flex items-center gap-1 no-print">
              <CheckCircle2 :size="14" />
              Validar Evidencia
            </button>
          </div>
        </fieldset>

        <!-- Section V: Transferencia -->
        <fieldset class="win95-outset p-4 mt-6">
          <legend class="px-2 font-bold bg-win95-bg">V. TRANSFERENCIA DE EVIDENCIA</legend>
          
          <div class="mb-4">
            <h4 class="text-[11px] font-bold mb-2">a. MOTIVO DE TRASLADO:</h4>
            <div class="grid grid-cols-2 sm:grid-cols-3 gap-2">
              <div v-for="(motivo, i) in ['Traslado', 'Peritaje', 'Resguardo', 'Disposición Judicial', 'Disposición Final']" :key="motivo" 
                   @click="toggleMotivo(motivo)"
                   class="flex items-center gap-2 cursor-pointer select-none">
                <div :class="['w-4 h-4 win95-inset flex items-center justify-center', motivos[motivo] ? 'bg-white' : 'bg-win95-highlight']">
                  <div v-if="motivos[motivo]" class="w-2 h-2 bg-black"></div>
                </div>
                <span class="text-[11px]">{{i + 1}}. {{motivo}}</span>
              </div>
            </div>
          </div>

          <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
            <div v-for="title in ['b. ENTREGA', 'c. RECIBE']" :key="title" class="win95-inset p-3 bg-win95-bg">
              <h4 class="text-[11px] font-bold bg-win95-title-bg text-white px-2 mb-3">{{title}}</h4>
              <div class="space-y-2 mb-4">
                <div v-for="label in ['Nombres y Apellidos', 'Organismo', 'Despacho', 'C.I./Cred', 'Fecha']" :key="label" class="flex flex-col gap-1">
                  <span class="text-[10px] font-bold tracking-tight">{{label}}:</span>
                  <input type="text" class="win95-input w-full" />
                </div>
              </div>
              <div class="grid grid-cols-3 gap-2">
                <div class="aspect-square bg-white win95-inset flex items-center justify-center text-[8px] font-bold text-win95-border-mid opacity-30 italic">FIRMA</div>
                <div class="aspect-square bg-white win95-inset flex items-center justify-center"><Fingerprint :size="16" class="opacity-10" /></div>
                <div class="aspect-square bg-white win95-inset flex items-center justify-center"><Fingerprint :size="16" class="opacity-10" /></div>
              </div>
            </div>
          </div>

          <div class="mt-4 pt-4 border-t-2 border-win95-border-mid">
            <h4 class="text-[11px] font-bold mb-2">d. OBSERVACIONES ADICIONALES:</h4>
            <textarea class="win95-input w-full h-20 resize-none"></textarea>
            <p class="mt-4 text-[9px] italic leading-tight text-win95-title-bg font-bold">
              IMPORTANTE: La planilla de Registro de Cadena de Custodia debe permanecer siempre con la evidencia, y sólo en original, desde el instante de su llenado en el lugar de obtención hasta la disposición final de la evidencia.
            </p>
          </div>
        </fieldset>
      </div>

      <!-- StatusBar -->
      <div class="flex win95-inset mt-4 text-[10px] bg-win95-bg divide-x-2 divide-win95-border-mid overflow-hidden no-print">
        <div class="px-2 py-0.5 flex-1 truncate italic">Para ayuda, pulse F1</div>
        <div class="px-2 py-0.5 w-24 text-center">NUM</div>
        <div class="px-2 py-0.5 w-24 text-center">SCRL</div>
        <div class="px-2 py-0.5 w-24 text-center uppercase">{{ new Date().toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'}) }}</div>
      </div>
    </div>

    <!-- START BAR / CONTROLS -->
    <div class="w-full fixed bottom-0 left-0 bg-win95-bg border-t-2 border-white win95-outset z-50 p-1 flex items-center justify-end no-print">
      <div class="flex items-center gap-2">
        <button 
          @click="printDoc"
          class="win95-button flex items-center gap-2 text-[11px]"
        >
          <Printer :size="16" />
          Imprimir Formulario
        </button>
        <div class="win95-inset px-2 py-0.5 bg-win95-bg text-[11px] flex items-center gap-2 ml-2">
          <CheckCircle2 :size="12" class="text-win95-text" />
          <span>Sistema Listo</span>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
@media print {
  @page {
    size: legal;
    margin-top: 2cm;
    margin-bottom: 2cm;
  }
}
</style>
