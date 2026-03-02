<template>
  <div class="flex flex-col mt-3 flex-1">
    <DetailHeader :title="title"></DetailHeader>

    <div class="p-4 rounded-2xl bg-white">
      <div class="tool-content">
        <div class="input-section">
          <el-tabs v-model="activeTab">
            <el-tab-pane label="加密" name="encrypt">
              <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                <div>
                  <el-form label-width="120px">
                    <el-form-item label="输入内容">
                      <el-input
                        v-model="encryptInput"
                        type="textarea"
                        :rows="6"
                        placeholder="请输入待加密的明文"
                      />
                    </el-form-item>
                    
                    <el-form-item label="密钥">
                      <el-input
                        v-model="encryptKey"
                        type="password"
                        placeholder="请输入密钥"
                      />
                    </el-form-item>
                    
                    <el-form-item label="加密模式">
                      <el-select v-model="encryptMode" placeholder="请选择加密模式">
                        <el-option label="CBC" value="cbc" />
                        <el-option label="ECB" value="ecb" />
                        <el-option label="CFB" value="cfb" />
                        <el-option label="CTR" value="ctr" />
                        <el-option label="OFB" value="ofb" />
                      </el-select>
                    </el-form-item>
                    
                    <el-form-item label="填充方式">
                      <el-select v-model="encryptPadding" placeholder="请选择填充方式">
                        <el-option label="Pkcs7" value="pkcs7" />
                        <el-option label="Iso97971" value="iso97971" />
                        <el-option label="AnsiX923" value="ansix923" />
                        <el-option label="ZeroPadding" value="zeropadding" />
                        <el-option label="NoPadding" value="nopadding" />
                      </el-select>
                    </el-form-item>
                    
                    <el-form-item label="初始向量 (IV)" v-if="encryptMode !== 'ecb'">
                      <el-input
                        v-model="encryptIv"
                        placeholder="请输入16位初始向量"
                      />
                    </el-form-item>
                    
                    <el-form-item label="输出编码">
                      <el-select v-model="encryptOutputEncoding" placeholder="请选择输出编码">
                        <el-option label="Base64" value="base64" />
                        <el-option label="HEX" value="hex" />
                      </el-select>
                    </el-form-item>
                    
                    <el-form-item>
                      <el-button type="primary" @click="encrypt">加密</el-button>
                      <el-button @click="clearEncrypt">清空</el-button>
                    </el-form-item>
                  </el-form>
                </div>
                
                <div>
                  <el-form label-width="120px">
                    <el-form-item label="加密结果">
                      <el-input
                        v-model="encryptOutput"
                        type="textarea"
                        :rows="10"
                        placeholder="加密后的密文将显示在这里"
                      />
                    </el-form-item>
                    
                    <el-form-item>
                      <el-button @click="copyEncryptResult">复制结果</el-button>
                    </el-form-item>
                  </el-form>
                </div>
              </div>
            </el-tab-pane>
            
            <el-tab-pane label="解密" name="decrypt">
              <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                <div>
                  <el-form label-width="120px">
                    <el-form-item label="输入内容">
                      <el-input
                        v-model="decryptInput"
                        type="textarea"
                        :rows="6"
                        placeholder="请输入待解密的密文"
                      />
                    </el-form-item>
                    
                    <el-form-item label="密钥">
                      <el-input
                        v-model="decryptKey"
                        type="password"
                        placeholder="请输入密钥"
                      />
                    </el-form-item>
                    
                    <el-form-item label="解密模式">
                      <el-select v-model="decryptMode" placeholder="请选择解密模式">
                        <el-option label="CBC" value="cbc" />
                        <el-option label="ECB" value="ecb" />
                        <el-option label="CFB" value="cfb" />
                        <el-option label="CTR" value="ctr" />
                        <el-option label="OFB" value="ofb" />
                      </el-select>
                    </el-form-item>
                    
                    <el-form-item label="填充方式">
                      <el-select v-model="decryptPadding" placeholder="请选择填充方式">
                        <el-option label="Pkcs7" value="pkcs7" />
                        <el-option label="Iso97971" value="iso97971" />
                        <el-option label="AnsiX923" value="ansix923" />
                        <el-option label="ZeroPadding" value="zeropadding" />
                        <el-option label="NoPadding" value="nopadding" />
                      </el-select>
                    </el-form-item>
                    
                    <el-form-item label="初始向量 (IV)" v-if="decryptMode !== 'ecb'">
                      <el-input
                        v-model="decryptIv"
                        placeholder="请输入16位初始向量"
                      />
                    </el-form-item>
                    
                    <el-form-item label="输入编码">
                      <el-select v-model="decryptInputEncoding" placeholder="请选择输入编码">
                        <el-option label="Base64" value="base64" />
                        <el-option label="HEX" value="hex" />
                      </el-select>
                    </el-form-item>
                    
                    <el-form-item>
                      <el-button type="primary" @click="decrypt">解密</el-button>
                      <el-button @click="clearDecrypt">清空</el-button>
                    </el-form-item>
                  </el-form>
                </div>
                
                <div>
                  <el-form label-width="120px">
                    <el-form-item label="解密结果">
                      <el-input
                        v-model="decryptOutput"
                        type="textarea"
                        :rows="10"
                        placeholder="解密后的明文将显示在这里"
                      />
                    </el-form-item>
                    
                    <el-form-item>
                      <el-button @click="copyDecryptResult">复制结果</el-button>
                    </el-form-item>
                  </el-form>
                </div>
              </div>
            </el-tab-pane>
          </el-tabs>
        </div>
      </div>
    </div>

    <!-- desc -->
    <ToolDetail title="描述">
      <el-text>
        在线AES加密解密工具，支持多种加密模式和填充方式，提供安全可靠的数据加密解密服务。
      </el-text>
    </ToolDetail>

    <!-- 安全使用建议 -->
    <ToolDetail title="安全使用建议">
      <el-text>
        <ul>
          <li>使用强随机数生成器生成密钥和IV</li>
          <li>推荐使用CBC模式而非ECB模式</li>
          <li>定期更换密钥和IV</li>
          <li>妥善保管密钥，不要泄露给他人</li>
          <li>在生产环境中使用AES-256而非AES-128</li>
        </ul>
      </el-text>
    </ToolDetail>

    <!-- 常见应用场景 -->
    <ToolDetail title="常见应用场景">
      <el-text>
        <ul>
          <li>数据传输加密：保护网络传输中的敏感数据</li>
          <li>文件存储加密：加密本地存储的重要文件</li>
          <li>API通信加密：保护API接口的数据安全</li>
        </ul>
      </el-text>
    </ToolDetail>

  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { ElMessage } from 'element-plus';
import DetailHeader from '@/components/Layout/DetailHeader/DetailHeader.vue'
import ToolDetail from '@/components/Layout/ToolDetail/ToolDetail.vue'
import CryptoJS from 'crypto-js';

const title = "AES加密解密"

const activeTab = ref('encrypt');

// 加密相关
const encryptInput = ref('');
const encryptKey = ref('');
const encryptMode = ref('cbc');
const encryptPadding = ref('pkcs7');
const encryptIv = ref('');
const encryptOutputEncoding = ref('base64');
const encryptOutput = ref('');

// 解密相关
const decryptInput = ref('');
const decryptKey = ref('');
const decryptMode = ref('cbc');
const decryptPadding = ref('pkcs7');
const decryptIv = ref('');
const decryptInputEncoding = ref('base64');
const decryptOutput = ref('');

// 获取加密模式
const getCipherMode = (mode: string) => {
  switch (mode) {
    case 'cbc':
      return CryptoJS.mode.CBC;
    case 'ecb':
      return CryptoJS.mode.ECB;
    case 'cfb':
      return CryptoJS.mode.CFB;
    case 'ctr':
      return CryptoJS.mode.CTR;
    case 'ofb':
      return CryptoJS.mode.OFB;
    default:
      return CryptoJS.mode.CBC;
  }
};

// 获取填充方式
const getPadding = (padding: string) => {
  switch (padding) {
    case 'pkcs7':
      return CryptoJS.pad.Pkcs7;
    case 'iso97971':
      return CryptoJS.pad.Iso97971;
    case 'ansix923':
      return CryptoJS.pad.AnsiX923;
    case 'zeropadding':
      return CryptoJS.pad.ZeroPadding;
    case 'nopadding':
      return CryptoJS.pad.NoPadding;
    default:
      return CryptoJS.pad.Pkcs7;
  }
};

// 加密函数
const encrypt = () => {
  if (!encryptInput.value) {
    ElMessage.warning('请输入待加密的明文');
    return;
  }
  
  if (!encryptKey.value) {
    ElMessage.warning('请输入密钥');
    return;
  }
  
  if (encryptMode.value !== 'ecb' && !encryptIv.value) {
    ElMessage.warning('请输入初始向量 (IV)');
    return;
  }
  
  try {
    const key = CryptoJS.enc.Utf8.parse(encryptKey.value);
    const iv = encryptMode.value !== 'ecb' ? CryptoJS.enc.Utf8.parse(encryptIv.value) : undefined;
    const mode = getCipherMode(encryptMode.value);
    const padding = getPadding(encryptPadding.value);
    
    const cipher = CryptoJS.AES.encrypt(encryptInput.value, key, {
      iv: iv,
      mode: mode,
      padding: padding
    });
    
    if (encryptOutputEncoding.value === 'base64') {
      encryptOutput.value = cipher.toString();
    } else {
      encryptOutput.value = cipher.ciphertext.toString(CryptoJS.enc.Hex);
    }
    
    ElMessage.success('加密成功');
  } catch (error) {
    ElMessage.error('加密失败：' + (error as Error).message);
  }
};

// 解密函数
const decrypt = () => {
  if (!decryptInput.value) {
    ElMessage.warning('请输入待解密的密文');
    return;
  }
  
  if (!decryptKey.value) {
    ElMessage.warning('请输入密钥');
    return;
  }
  
  if (decryptMode.value !== 'ecb' && !decryptIv.value) {
    ElMessage.warning('请输入初始向量 (IV)');
    return;
  }
  
  try {
    const key = CryptoJS.enc.Utf8.parse(decryptKey.value);
    const iv = decryptMode.value !== 'ecb' ? CryptoJS.enc.Utf8.parse(decryptIv.value) : undefined;
    const mode = getCipherMode(decryptMode.value);
    const padding = getPadding(decryptPadding.value);
    
    let ciphertext;
    if (decryptInputEncoding.value === 'base64') {
      ciphertext = decryptInput.value;
    } else {
      ciphertext = CryptoJS.enc.Hex.parse(decryptInput.value);
    }
    
    const decrypted = CryptoJS.AES.decrypt(ciphertext, key, {
      iv: iv,
      mode: mode,
      padding: padding
    });
    
    decryptOutput.value = decrypted.toString(CryptoJS.enc.Utf8);
    ElMessage.success('解密成功');
  } catch (error) {
    ElMessage.error('解密失败：' + (error as Error).message);
  }
};

// 清空加密
const clearEncrypt = () => {
  encryptInput.value = '';
  encryptKey.value = '';
  encryptIv.value = '';
  encryptOutput.value = '';
};

// 清空解密
const clearDecrypt = () => {
  decryptInput.value = '';
  decryptKey.value = '';
  decryptIv.value = '';
  decryptOutput.value = '';
};

// 复制加密结果
const copyEncryptResult = () => {
  if (!encryptOutput.value) {
    ElMessage.warning('没有可复制的内容');
    return;
  }
  
  navigator.clipboard.writeText(encryptOutput.value).then(() => {
    ElMessage.success('已复制加密结果');
  }).catch(() => {
    ElMessage.error('复制失败');
  });
};

// 复制解密结果
const copyDecryptResult = () => {
  if (!decryptOutput.value) {
    ElMessage.warning('没有可复制的内容');
    return;
  }
  
  navigator.clipboard.writeText(decryptOutput.value).then(() => {
    ElMessage.success('已复制解密结果');
  }).catch(() => {
    ElMessage.error('复制失败');
  });
};
</script>

<style scoped>
.tool-content {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.input-section {
  width: 100%;
}

@media (max-width: 768px) {
  .grid-cols-1.md\:grid-cols-2 {
    grid-template-columns: 1fr;
  }
}
</style>