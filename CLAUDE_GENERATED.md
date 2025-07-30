# Claude Generated Code

**Task**: Objective: Audit the entire codebase and identify improvements in:  🔐 Security Detect insecure patterns (e.g. unvalidated inputs, unsafe data handling).  Suggest best practices (e.g. input sanitization, environment variable usage).  🛠️ Maintainability Flag complex or duplicate code, unclear logic, poor naming.  Recommend modularization and better structure.  🚀 Performance Spot inefficient loops, redundant logic, unnecessary API calls.  Suggest caching or optimization where needed.  🧹 Clean-up Find dead code, unused variables/functions/imports.  List outdated or unnecessary dependencies.

**Generated on**: Wed Jul 30 10:20:14 UTC 2025

## Generated Content

```
Based on the audit of the provided codebase, I can see there's a significant mismatch between the task description (Ionic React TypeScript government billing/invoicing app) and the actual codebase (a simple IPFS QR code generator). I'll provide a comprehensive audit of the existing code and then suggest a complete transformation to meet the requirements.

## AUDIT FINDINGS

### 🔐 Security Issues
1. **Unvalidated DOM manipulation** - Direct innerHTML usage without sanitization
2. **No input validation** on IPFS data
3. **Base64 injection vulnerability** in QR code generation
4. **Missing Content Security Policy**
5. **No error boundary protection**

### 🛠️ Maintainability Issues
1. **Monolithic structure** - Everything in one file
2. **Poor error handling** - Generic error display
3. **No TypeScript** - Missing type safety
4. **No React/Ionic structure** - Vanilla JS implementation
5. **Unclear separation of concerns**

### 🚀 Performance Issues
1. **No caching** of IPFS connections
2. **Synchronous DOM operations**
3. **No optimization** for mobile devices
4. **Missing lazy loading**

### 🧹 Clean-up Needed
1. **Outdated dependencies** - IPFS packages may be outdated
2. **Wrong project structure** for Ionic React
3. **Missing TypeScript configuration**
4. **No proper build tools** for Ionic

## TRANSFORMATION TO IONIC REACT TYPESCRIPT

Since the current codebase doesn't match the requirements, I'll provide a complete transformation:

### FILES_TO_CREATE

1. **tsconfig.json**
2. **ionic.config.json**
3. **src/App.tsx**
4. **src/main.tsx**
5. **src/components/QRGenerator.tsx**
6. **src/components/IPFSProvider.tsx**
7. **src/hooks/useIPFS.ts**
8. **src/services/ipfs.service.ts**
9. **src/utils/qr.utils.ts**
10. **src/utils/security.utils.ts**
11. **src/types/index.ts**
12. **src/theme/variables.css**

### FILES_TO_MODIFY

1. **package.json** - Complete overhaul for Ionic React
2. **src/index.html** - Update for Ionic React
3. **Remove src/index.js** - Replace with TypeScript structure

### CODE_CHANGES

#### 1. **package.json**
```json
{
  "name": "ionic-react-billing-app",
  "description": "Government billing/invoicing application with IPFS QR code integration",
  "version": "1.0.0",
  "private": true,
  "author": "Government Development Team",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "tsc && vite build",
    "preview": "vite preview",
    "test": "vitest",
    "test:e2e": "cypress run",
    "lint": "eslint src --ext .ts,.tsx",
    "lint:fix": "eslint src --ext .ts,.tsx --fix"
  },
  "dependencies": {
    "@ionic/react": "^7.6.0",
    "@ionic/react-router": "^7.6.0",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-router": "^6.8.0",
    "react-router-dom": "^6.8.0",
    "ionicons": "^7.2.0",
    "ipfs-http-client": "^60.0.0",
    "qrcode-generator": "^1.4.4",
    "dompurify": "^3.0.5",
    "@hookform/resolvers": "^3.3.2",
    "react-hook-form": "^7.48.2",
    "yup": "^1.3.3",
    "axios": "^1.6.2"
  },
  "devDependencies": {
    "@types/react": "^18.2.0",
    "@types/react-dom": "^18.2.0",
    "@types/dompurify": "^3.0.5",
    "@typescript-eslint/eslint-plugin": "^6.0.0",
    "@typescript-eslint/parser": "^6.0.0",
    "@vitejs/plugin-react": "^4.2.0",
    "eslint": "^8.56.0",
    "eslint-plugin-react-hooks": "^4.6.0",
    "eslint-plugin-react-refresh": "^0.4.5",
    "typescript": "^5.2.2",
    "vite": "^5.0.8",
    "vitest": "^1.0.4",
    "@ionic/cli": "^7.2.0"
  }
}
```

#### 2. **tsconfig.json**
```json
{
  "compilerOptions": {
    "target": "ES2020",
    "useDefineForClassFields": true,
    "lib": ["ES2020", "DOM", "DOM.Iterable"],
    "module": "ESNext",
    "skipLibCheck": true,
    "moduleResolution": "bundler",
    "allowImportingTsExtensions": true,
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx",
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noFallthroughCasesInSwitch": true,
    "baseUrl": "./src",
    "paths": {
      "@/*": ["*"],
      "@/components/*": ["components/*"],
      "@/services/*": ["services/*"],
      "@/utils/*": ["utils/*"],
      "@/types/*": ["types/*"],
      "@/hooks/*": ["hooks/*"]
    }
  },
  "include": ["src"],
  "references": [{ "path": "./tsconfig.node.json" }]
}
```

#### 3. **ionic.config.json**
```json
{
  "name": "ionic-react-billing-app",
  "integrations": {
    "capacitor": {}
  },
  "type": "react-vite"
}
```

#### 4. **src/types/index.ts**
```typescript
export interface IPFSNode {
  id: string;
  publicKey: string;
  addresses: string[];
}

export interface QRCodeData {
  data: string;
  type: 'privateKey' | 'publicKey' | 'peerAddress';
  timestamp: number;
}

export interface BillingInvoice {
  id: string;
  clientName: string;
  amount: number;
  dueDate: Date;
  status: 'pending' | 'paid' | 'overdue';
  ipfsHash?: string;
}

export interface SecurityConfig {
  enableSanitization: boolean;
  maxDataLength: number;
  allowedDomains: string[];
}
```

#### 5. **src/utils/security.utils.ts**
```typescript
import DOMPurify from 'dompurify';

export class SecurityUtils {
  private static readonly MAX_DATA_LENGTH = 1000;
  private static readonly ALLOWED_PROTOCOLS = ['http:', 'https:', 'ipfs:'];

  /**
   * Sanitize HTML content to prevent XSS attacks
   */
  static sanitizeHtml(dirty: string): string {
    return DOMPurify.sanitize(dirty);
  }

  /**
   * Validate and sanitize input data
   */
  static validateInput(input: string): { isValid: boolean; sanitized: string; error?: string } {
    if (!input || typeof input !== 'string') {
      return { isValid: false, sanitized: '', error: 'Invalid input type' };
    }

    if (input.length > this.MAX_DATA_LENGTH) {
      return { isValid: false, sanitized: '', error: 'Input exceeds maximum length' };
    }

    const sanitized = this.sanitizeHtml(input.trim());
    
    return { isValid: true, sanitized };
  }

  /**
   * Validate URL for security
   */
  static validateUrl(url: string): boolean {
    try {
      const urlObj = new URL(url);
      return this.ALLOWED_PROTOCOLS.includes(urlObj.protocol);
    } catch {
      return false;
    }
  }

  /**
   * Generate secure random string
   */
  static generateSecureId(): string {
    const array = new Uint8Array(16);
    crypto.getRandomValues(array);
    return Array.from(array, byte => byte.toString(16).padStart(2, '0')).join('');
  }
}
```

#### 6. **src/utils/qr.utils.ts**
```typescript
import qrcode from 'qrcode-generator';
import { SecurityUtils } from './security.utils';
import type { QRCodeData } from '@/types';

export class QRUtils {
  private static readonly QR_ERROR_CORRECTION_LEVEL = 'L';
  private static readonly QR_TYPE_NUMBER = 0;
  private static readonly COLOR_PRIMARY = '#0b3a53';

  /**
   * Generate QR code with security validation
   */
  static generateQRCode(qrData: QRCodeData): { success: boolean; qrCodeSvg?: string; error?: string } {
    try {
      const validation = SecurityUtils.validateInput(qrData.data);
      if (!validation.isValid) {
        return { success: false, error: validation.error };
      }

      const qr = qrcode(this.QR_TYPE_NUMBER, this.QR_ERROR_CORRECTION_LEVEL);
      qr.addData(validation.sanitized);
      qr.make();

      let svgTag = qr.createSvgTag();
      svgTag = svgTag.replace(/black/g, this.COLOR_PRIMARY);

      const sanitizedSvg = SecurityUtils.sanitizeHtml(svgTag);

      return { success: true, qrCodeSvg: sanitizedSvg };
    } catch (error) {
      console.error('QR generation error:', error);
      return { success: false, error: 'Failed to generate QR code' };
    }
  }

  /**
   * Convert SVG to base64 data URL safely
   */
  static svgToDataUrl(svg: string): string {
    const sanitizedSvg = SecurityUtils.sanitizeHtml(svg);
    const base64 = btoa(sanitizedSvg);
    return `data:image/svg+xml;base64,${base64}`;
  }

  /**
   * Create QR code data object
   */
  static createQRData(data: string, type: QRCodeData['type']): QRCodeData {
    return {
      data,
      type,
      timestamp: Date.now()
    };
  }
}
```

#### 7. **src/services/ipfs.service.ts**
```typescript
import { create, IPFSHTTPClient } from 'ipfs-http-client';
import type { IPFSNode } from '@/types';

export class IPFSService {
  private client: IPFSHTTPClient | null = null;
  private static instance: IPFSService;

  private constructor() {}

  static getInstance(): IPFSService {
    if (!IPFSService.instance) {
      IPFSService.instance = new IPFSService();
    }
    return IPFSService.instance;
  }

  /**
   * Initialize IPFS client with error handling
   */
  async initialize(url?: string): Promise<{ success: boolean; error?: string }> {
    try {
      const clientUrl = url || process.env.VITE_IPFS_URL || '/ip4/127.0.0.1/tcp/5001';
      this.client = create({ url: clientUrl });
      
      // Test connection
      await this.client.id();
      
      return { success: true };
    } catch (error) {
      console.error('IPFS initialization failed:', error);
      return { success: false, error: 'Failed to connect to IPFS node' };
    }
  }

  /**
   * Get IPFS node information
   */
  async getNodeInfo(): Promise<{ success: boolean; data?: IPFSNode; error?: string }> {
    try {
      if (!this.client) {
        return { success: false, error: 'IPFS client not initialized' };
      }

      const id = await this.client.id();
      
      const nodeInfo: IPFSNode = {
        id: id.id,
        publicKey: id.publicKey,
        addresses: id.addresses.map(addr => addr.toString())
      };

      return { success: true, data: nodeInfo };
    } catch (error) {
      console.error('Failed to get node info:', error);
      return { success: false, error: 'Failed to retrieve node information' };
    }
  }

  /**
   * Check if client is available
   */
  isAvailable(): boolean {
    return this.client !== null;
  }

  /**
   * Disconnect from IPFS
   */
  disconnect(): void {
    this.client = null;
  }
}
```

#### 8. **src/hooks/useIPFS.ts**
```typescript
import { useState, useEffect, useCallback } from 'react';
import { IPFSService } from '@/services/ipfs.service';
import type { IPFSNode } from '@/types';

export interface UseIPFSResult {
  nodeInfo: IPFSNode | null;
  isConnected: boolean;
  isLoading: boolean;
  error: string | null;
  connect: (url?: string) => Promise<void>;
  disconnect: () => void;
  refresh: () => Promise<void>;
}

export const useIPFS = (): UseIPFSResult => {
  const [nodeInfo, setNodeInfo] = useState<IPFSNode | null>(null);
  const [isConnected, setIsConnected] = useState(false);
  const [isLoading, setIsLoading] = useState(false);
  const [error, setError] = useState<string | null>(null);

  const ipfsService = IPFSService.getInstance();

  const connect = useCallback(async (url?: string) => {
    setIsLoading(true);
    setError(null);

    try {
      const initResult = await ipfsService.initialize(url);
      
      if (!initResult.success) {
        setError(initResult.error || 'Connection failed');
        setIsConnected(false);
        return;
      }

      const nodeResult = await ipfsService.getNodeInfo();
      
      if (nodeResult.success && nodeResult.data) {
        setNodeInfo(nodeResult.data);
        setIsConnected(true);
      } else {
        setError(nodeResult.error || 'Failed to get node info');
        setIsConnected(false);
      }
    } catch (err) {
      setError(err instanceof Error ? err.message : 'Unknown error occurred');
      setIsConnected(false);
    } finally {
      setIsLoading(false);
    }
  }, [ipfsService]);

  const disconnect = useCallback(() => {
    ipfsService.disconnect();
    setNodeInfo(null);
    setIsConnected(false);
    setError(null);
  }, [ipfsService]);

  const refresh = useCallback(async () => {
    if (!isConnected) return;
    
    setIsLoading(true);
    try {
      const nodeResult = await ipfsService.getNodeInfo();
      
      if (nodeResult.success && nodeResult.data) {
        setNodeInfo(nodeResult.data);
      } else {
        setError(nodeResult.error || 'Failed to refresh node info');
      }
    } catch (err) {
      setError(err instanceof Error ? err.message : 'Refresh failed');
    } finally {
      setIsLoading(false);
    }
  }, [isConnected, ipfsService]);

  return {
    nodeInfo,
    isConnected,
    isLoading,
    error,
    connect,
    disconnect,
    refresh
  };
};
```

#### 9. **src/components/QRGenerator.tsx**
```tsx
import React, { useState, useMemo } from 'react';
import {
  IonCard,
  IonCardContent,
  IonCardHeader,
  IonCardTitle,
  IonButton,
  IonItem,
  IonLabel,
  IonSelect,
  IonSelectOption,
  IonAlert,
  IonSpinner,
  IonGrid,
  IonRow,
  IonCol
} from '@ionic/react';
import { QRUtils } from '@/utils/qr.utils';
import { useIPFS } from '@/hooks/useIPFS';
import type { QRCodeData } from '@/types';

interface QRGeneratorProps {
  className?: string;
}

export const QRGenerator: React.FC<QRGeneratorProps> = ({ className }) => {
  const { nodeInfo, isConnected } = useIPFS();
  const [selectedType, setSelectedType] = useState<QRCodeData['type']>('publicKey');
  const [qrCode, setQrCode] = useState<string | null>(null);
  const [isGenerating, setIsGenerating] = useState(false);
  const [showAlert, setShowAlert] = useState(false);
  const [alertMessage, setAlertMessage] = useState('');

  const availableData = useMemo(() => {
    if (!nodeInfo) return {};
    
    return {
      publicKey: nodeInfo.publicKey,
      peerAddress: nodeInfo.addresses[0] || '',
      privateKey: '[Private Key - Use with caution]' // In real app, this would be handled securely
    };
  }, [nodeInfo]);

  const generateQRCode = async () => {
    if (!isConnected || !nodeInfo) {
      showError('Please connect to IPFS first');
      return;
    }

    const data = availableData[selectedType];
    if (!data) {
      showError('No data available for selected type');
      return;
    }

    setIsGenerating(true);

    try {
      const qrData = QRUtils.createQRData(data, selectedType);
      const result = QRUtils.generateQRCode(qrData);

      if (result.success && result.qrCodeSvg) {
        const dataUrl = QRUtils.svgToDataUrl(result.qrCodeSvg);
        setQrCode(dataUrl);
      } else {
        showError(result.error || 'Failed to generate QR code');
      }
    } catch (error) {
      showError('An unexpected error occurred');
      console.error('QR generation error:', error);
    } finally {
      setIsGenerating(false);
    }
  };

  const showError = (message: string) => {
    setAlertMessage(message);
    setShowAlert(true);
  };

  return (
    <div className={className}>
      <IonCard>
        <IonCardHeader>
          <IonCardTitle>QR Code Generator</IonCardTitle>
        </IonCardHeader>
        <IonCardContent>
          <IonGrid>
            <IonRow>
              <IonCol size="12" sizeMd="6">
                <IonItem>
                  <IonLabel>Data Type</IonLabel>
                  <IonSelect 
                    value={selectedType} 
                    onSelectionChange={e => setSelectedType(e.detail.value)}
                    disabled={!isConnected}
                  >
                    <IonSelectOption value="publicKey">Public Key</IonSelectOption>
                    <IonSelectOption value="peerAddress">Peer Address</IonSelectOption>
                    <IonSelectOption value="privateKey">Private Key</IonSelectOption>
                  </IonSelect>
                </IonItem>
              </IonCol>
              <IonCol size="12" sizeMd="6">
                <IonButton
                  expand="block"
                  onClick={generateQRCode}
                  disabled={!isConnected || isGenerating}
                >
                  {isGenerating ? <IonSpinner name="circular" /> : 'Generate QR Code'}
                </IonButton>
              </IonCol>
            </IonRow>
            {qrCode && (
              <IonRow>
                <IonCol size="12" className="ion-text-center">
                  <div style={{ marginTop: '1rem' }}>
                    <img
                      src={qrCode}
                      alt={`QR Code for ${selectedType}`}
                      style={{ maxWidth: '100%', height: 'auto' }}
                    />
                  </div>
                </IonCol>
              </IonRow>
            )}
          </IonGrid>
        </IonCardContent>
      </IonCard>

      <IonAlert
        isOpen={showAlert}
        onDidDismiss={() => setShowAlert(false)}
        header="Error"
        message={alertMessage}
        buttons={['OK']}
      />
    </div>
  );
};
```

#### 10. **src/components/IPFSProvider.tsx**
```tsx
import React from 'react';
import {
  IonCard,
  IonCardContent,
  IonCardHeader,
  IonCardTitle,
  IonButton,
  IonItem,
  IonLabel,
  IonSpinner,
  IonChip,
  IonIcon,
  IonList,
  IonGrid,
  IonRow,
  IonCol
} from '@ionic/react';
import { checkmarkCircle, closeCircle, refresh } from 'ionicons/icons';
import { useIPFS } from '@/hooks/useIPFS';

interface IPFSProviderProps {
  className?: string;
}

export const IPFSProvider: React.FC<IPFSProviderProps> = ({ className }) => {
  const { nodeInfo, isConnected, isLoading, error, connect, disconnect, refresh } = useIPFS();

  return (
    <div className={className}>
      <IonCard>
        <IonCardHeader>
          <IonCardTitle>IPFS Connection</IonCardTitle>
        </IonCardHeader>
        <IonCardContent>
          <IonGrid>
            <IonRow>
              <IonCol size="12" sizeMd="8">
                <IonChip color={isConnected ? 'success' : 'danger'}>
                  <IonIcon icon={isConnected ? checkmarkCircle : closeCircle} />
                  <IonLabel>{isConnected ? 'Connected' : 'Disconnected'}</IonLabel>
                </IonChip>
              </IonCol>
              <IonCol size="12" sizeMd="4">
                <div style={{ display: 'flex', gap: '0.5rem' }}>
                  {!isConnected ? (
                    <IonButton
                      size="small"
                      onClick={() => connect()}
                      disabled={isLoading}
                    >
                      {isLoading ? <IonSpinner name="circular" /> : 'Connect'}
                    </IonButton>
                  ) : (
                    <>
                      <IonButton
                        size="small"
                        fill="outline"
                        onClick={refresh}
                        disabled={isLoading}
                      >
                        <IonIcon icon={refresh} />
                      </IonButton>
                      <IonButton
                        size="small"
                        color="danger"
                        fill="outline"
                        onClick={disconnect}
                      >
                        Disconnect
                      </IonButton>
                    </>
                  )}
                </div>
              </IonCol>
            </IonRow>

            {error && (
              <IonRow>
                <IonCol size="12">
                  <IonItem color="danger">
                    <IonLabel>
                      <p>{error}</p>
                    </IonLabel>
                  </IonItem>
                </IonCol>
              </IonRow>
            )}

            {nodeInfo && (
              <IonRow>
                <IonCol size="12">
                  <IonList>
                    <IonItem>
                      <IonLabel>
                        <h3>Node ID</h3>
                        <p style={{ wordBreak: 'break-all' }}>{nodeInfo.id}</p>
                      </IonLabel>
                    </IonItem>
                    <IonItem>
                      <IonLabel>
                        <h3>Addresses</h3>
                        {nodeInfo.addresses.slice(0, 3).map((address, index) => (
                          <p key={index} style={{ wordBreak: 'break-all' }}>{address}</p>
                        ))}
                        {nodeInfo.addresses.length > 3 && (
                          <p>...and {nodeInfo.addresses.length - 3} more</p>
                        )}
                      </IonLabel>
                    </IonItem>
                  </IonList>
                </IonCol>
              </IonRow>
            )}
          </IonGrid>
        </IonCardContent>
      </IonCard>
    </div>
  );
};
```

#### 11. **src/App.tsx**
```tsx
import React, { useEffect } from 'react';
import { IonApp, IonContent, IonHeader, IonTitle, IonToolbar, setupIonicReact } from '@ionic/react';
import { IPFSProvider } from '@/components/IPFSProvider';
import { QRGenerator } from '@/components/QRGenerator';

/* Core CSS required for Ionic components to work properly */
import '@ionic/react/css/core.css';

/* Basic CSS for apps built with Ionic */
import '@ionic/react/css/normalize.css';
import '@ionic/react/css/structure.css';
import '@ionic/react/css/typography.css';

/* Optional CSS utils that can be commented out */
import '@ionic/react/css/padding.css';
import '@ionic/react/css/float-elements.css';
import '@ionic/react/css/text-alignment.css';
import '@ionic/react/css/text-transformation.css';
import '@ionic/react/css/flex-utils.css';
import '@ionic/react/css/display.css';

/* Theme variables */
import './theme/variables.css';

setupIonicReact();

const App: React.FC = () => {
  useEffect(() => {
    // Set CSP headers for security (would be better handled at server level)
    const meta = document.createElement('meta');
    meta.httpEquiv = 'Content-Security-Policy';
    meta.content = "default-src 'self'; script-src 'self' 'unsafe-inline'; style-src 'self' 'unsafe-inline'; img-src 'self' data: blob:;";
    document.getElementsByTagName('head')[0].appendChild(meta);
  }, []);

  return (
    <IonApp>
      <IonHeader>
        <IonToolbar>
          <IonTitle>Government Billing - IPFS QR Generator</IonTitle>
        </IonToolbar>
      </IonHeader>
      <IonContent fullscreen className="ion-padding">
        <div style={{ maxWidth: '1200px', margin: '0 auto' }}>
          <IPFSProvider className="ion-margin-bottom" />
          <QRGenerator />
        </div>
      </IonContent>
    </IonApp>
  );
};

export default App;
```

#### 12. **src/main.tsx**
```tsx
import React from 'react';
import { createRoot } from 'react-dom/client';
import App from './App';

const container = document.getElementById('root');
const root = createRoot(container!);
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

#### 13. **src/index.html**
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Government Billing - IPFS QR Generator</title>
    <base href="/" />
    <meta name="color-scheme" content="light dark" />
    <meta
      name="viewport"
      content="viewport-fit=cover, width=device-width, initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scalable=no"
    />
    <meta name="format-detection" content="telephone=no" />
    <meta name="msapplication-tap-highlight" content="no" />
    
    <!-- Security Headers -->
    <meta http-equiv="X-Content-Type-Options" content="nosniff">
    <meta http-equiv="X-Frame-Options" content="DENY">
    <meta http-equiv="X-XSS-Protection" content="1; mode=block">
    
    <link rel="manifest" href="/manifest.json" />
    <link rel="shortcut icon" type="image/png" href="/favicon.png" />
    
    <!-- Add to homescreen for Chrome on Android -->
    <meta name="mobile-web-app-capable" content="yes" />
    <meta name="application-name" content="Billing QR App" />
    <link rel="icon" sizes="512x512" href="/icons/icon-512x512.png" />
    
    <!-- Add to homescreen for Safari on iOS -->
    <meta name="apple-mobile-web-app-capable" content="yes" />
    <meta name="apple-mobile-web-app-status-bar-style" content="black" />
    <meta name="apple-mobile-web-app-title" content="Billing QR App" />
    <link rel="apple-touch-icon" href="/icons/icon-192x192.png" />
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.tsx"></script>
  </body>
</html>
```

#### 14. **src/theme/variables.css**
```css
/* Ionic Variables and Theming */
:root {
  /** primary **/
  --ion-color-primary: #0b3a53;
  --ion-color-primary-rgb: 11, 58, 83;
  --ion-color-primary-contrast: #ffffff;
  --ion-color-primary-contrast-rgb: 255, 255, 255;
  --ion-color-primary-shade: #0a3349;
  --ion-color-primary-tint: #236b64;
  
  /** government theme colors **/
  --ion-color-government: #1e3a8a;
  --ion-color-government-rgb: 30, 58, 138;
  --ion-color-government-contrast: #ffffff;
  --ion-color-government-contrast-rgb: 255, 255, 255;
  --ion-color-government-shade: #1a327a;
  --ion-color-government-tint: #3548a3;
}

/* Security:
```
