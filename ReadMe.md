## ���
����Ŀ����[CSRedis](https://github.com/Vip56/csredis)������Դ��Ĵ����޸���ɾ�����ṩ���ճ�����Ĳ�����ͬʱ��������
`Microsoft.Extensions.Caching.Abstractions`�⣬�Ӷ�������SDK�ܹ����ǵ�`.Net Core`�������Ӷ�������ͬ`.Net Core`
������Ҫ���е������Ӷ�ͳһ�汾��   

[![Build status](https://ci.appveyor.com/api/projects/status/9an7h8nk47eeod05/branch/master?svg=true)](https://ci.appveyor.com/project/vip56/sino-extensions-redis/branch/master)
[![NuGet](https://img.shields.io/nuget/v/Nuget.Core.svg?style=plastic)](https://www.nuget.org/packages/Sino.Extensions.Redis)
  
## ���ʹ��
�����������Ҫ��`Asp.Net Core`�����н���ʹ�ã��ÿ��Ѿ����õ�IOCע�룬�����߽���Ҫͨ�����·�ʽ����ע�뼴�ɣ�
```
services.AddRedisCache(Action<RedisCacheOptions> setupAction);
```
����`RedisCacheOptions`�����������²�����   

* RedisCacheOptions.Host��Redis�����ַ   
* RedisCacheOptions.Port��Redis����˿�   
* RedisCacheOptions.Password��Redis����   
* RedisCacheOptions.InstanceName��Keyǰ׺   

������Ϸ���ע�������Ҫʹ�õĵط�ͨ���ӿ�`IRedisCache`���ɷ��ʶ�Ӧ�ķ��񣬵�ǰ�ýӿڹ��������²���������   
```
// ����Key���������ַ���
string Get(string key);
Task<string> GetAsync(string key);

// �ж�key�Ƿ����
bool Exists(string key);
Task<bool> ExistsAsync(string key);

// ��������Key�ĳ�ʱʱ��
void Refresh(string key, int timeout);
Task RefreshAsync(string key, int timeout);

// ����Key�ĳ�ʱʱ�䣬��λ��
bool Expire(string key, int seconds);
Task<bool> ExpireAsync(string key, int seconds);

// ����Key�ĳ�ʱʱ�䣬��λ����
bool PExpire(string key, long milliseconds);
Task<bool> PExpireAsync(string key, long milliseconds);

// �Ƴ�Key
void Remove(string key);
Task RemoveAsync(string key);

// ����Key��ֵ
void Set(string key, string value, int? timeout = null);
Task SetAsync(string key, string value, int? timeout = null);

// ����Key��������������ֵ
bool SetNx(string key, string value);
Task<bool> SetNxAsync(string key, string value);

/// ��value׷�ӵ�keyֵ�󣬲��������ͬset
long Append(string key, string value);
Task<long> AppendAsync(string key, string value);

// ����key���洢���ַ�����
long StrLen(string key);
Task<long> StrLenAsync(string key);

// ��ȡkey�ַ��������ַ���
string GetRange(string key, long start, long end);
Task<string> GetRangeAsync(string key, long start, long end);

// ��������ַ����б�����Ϊ1�ı���λ����
long BitCount(string key, long? start = null, long? end = null);
Task<long> BitCountAsync(string key, long? start = null, long? end = null);

// ��Key��������ַ���ֵ���û����ָ��ƫ�����ϵ�λ
bool SetBit(string key, uint offset, bool value);
Task<bool> SetBitAsync(string key, uint offset, bool value);

// ��ȡKey�洢���ַ�����ָ��ƫ������λ
bool GetBit(string key, uint offset);
Task<bool> GetBitAsync(string key, uint offset);

// ��Key�д��������ֵ��һ
long Decr(string key);
Task<long> DecrAsync(string key);

// ��Key�д�������ּ��ٹ̶�ֵ
long DecrBy(string key, long decrement);
Task<long> DecrByAsync(string key, long decrement);

// ��Key�д������������һ
long Incr(string key);
Task<long> IncrAsync(string key);

// ��Key�д������������ֵ
long IncrBy(string key, long increment);
Task<long> IncrByAsync(string key, long increment);

// ɾ����ϣ��Key�е�һ������ָ����
long HDel(string key, params string[] fields);
Task<long> HDelAsync(string key, params string[] fields);

// �鿴��ϣ��Key�и�����field�Ƿ����
bool HExists(string key, string field);
Task<bool> HExistsAsync(string key, string field);

// ���ع�ϣ��Key��ָ�����ֵ
string HGet(string key, string field);
Task<string> HGetAsync(string key, string field);

// ���ع�ϣ��Key���������
long HLen(string key);
Task<long> HLenAsync(string key);

// ����ϣ��Key�е����ֵ����Ϊvalue
bool HSet(string key, string field, string value);
Task<bool> HSetAsync(string key, string field, string value);

// ����ϣKey�е����ֵ����ΪValue�����ҽ�����field������
bool HSetNx(string key, string field, string value);
Task<bool> HSetNxAsync(string key, string field, string value);

// ��������ģʽ��ȡָ��Key����������ֵ
Tuple<string, string> BLPop(int timeout, params string[] keys);
Task<Tuple<string, string>> BLPopAsync(int timeout, params string[] keys);

// �Ƴ��������б�key��ͷԪ��
string LPop(string key);
Task<string> LPopAsync(string key);

// ��������ģʽ��ȡָ��Key����������ֵ�������ʱ�򷵻�RedisProtocolException�쳣��
Tuple<string, string> BRPop(int timeout, params string[] keys);
Task<Tuple<string, string>> BRPopAsync(int timeout, params string[] keys);

// �����б�Key��ָ���±��Ԫ��
string LIndex(string key, long index);
Task<string> LIndexAsync(string key, long index);

// �����б�Key�ĳ���
long LLen(string key);
Task<long> LLenAsync(string key);

// ��һ������ֵ���뵽�б�key�ı�ͷ
long LPush(string key, params string[] values);
Task<long> LPushAsync(string key, params string[] values);

// ����key������Ϊ�б���value�����ͷ
long LPushX(string key, string value);
Task<long> LPushXAsync(string key, string value);

// �Ƴ��������б�key��βԪ��
string RPop(string key);
Task<string> RPopAsync(string key);

// ��һ������ֵ���뵽�б�β��
long RPush(string key, params string[] values);
Task<long> RPushAsync(string key, params string[] values);

// ����key������Ϊ�б���ֵ���뵽��β��
long RPushX(string key, params string[] values);
Task<long> RPushXAsync(string key, params string[] values);

// ��������ģʽ��ȡsource�б��е�ĩβԪ�أ�����
// ��ͬʱ������ӵ�destination��ͷ�������source
// �������κ�������ȴ���ֱ��ָ����timeout��ʱ��
string BRPopLPush(string source, string destination, int timeout);
Task<string> BRPopLPushAsync(string source, string destination, int timeout);

// ���б�source�����һ��Ԫ�ص��������أ�ͬʱ��
// ���Ԫ����ӵ�destination�б��ͷԪ�ء�
string RPopLPush(string source, string destination);
Task<string> RPopLPushAsync(string source, string destination);

// �Ƴ��б�key��count�������value��ȵ�Ԫ�أ����
// count����0��ӱ�ͷ��ʼ���β���������countС��0
// ��ӱ�β���ͷ������countΪ0���Ƴ����С�
long LRem(string key, long count, string value);
Task<long> LRemAsync(string key, long count, string value);
```   

�����������Ҫͨ�������ķ�ʽʹ�ã�����ֱ��ʹ��`PoolRedisClient`����ֱ�ӽ���ʹ�ã�ֻ��Ҫ�������·�ʽ
���г�ʼ�����ɣ�
```
var client = new RedisCache(new RedisCacheOptions
{
	Host = "127.0.0.1",
	Port = 6379,
	InstanceName = "console_"
});
```   

## ��Ŀ���

### ��Ŀ�ṹ
* Sino.Extensions.Redis��������⣻
* RedisUnitTest����Ԫ���ԣ�
* RedisConsole��ʵ�����Ӳ��ԣ�
    
### ��Ҫ�ṹ
���ǵ�ʵ��ʹ����Ŀ���еĴ�����ɾ�����ع���������Ŀ�Ƚ�С�ɣ��������ڵ�������չ����Ҫ��Ŀ¼�ṹ������ʾ��
* Commands������Redis����ľ��ڸ��ļ����£�
* Internal����Ҫ����Socket�������Լ��ֽ����ķ����Լ����գ�
* Types��Redis��������Ҫʹ�õ�ö�ٲ���ֵ��
* Utils����չ�ٷ��࣬���ڿ�����   

### ������   
Ϊ���ÿ����߿����˽���Ŀ�Ӷ��������֣���صĺ����ཫ����н��ܣ����ڿ����߽��в��ң�   

#### RedisCache��
������Ҫʵ����`IRedisCache`�ӿڣ��ṩ��`Asp.Net Core`��Ŀ�½���ʹ�ã�ͬʱ����ʵ����Ŀʹ�õľ��齫�����õ�
Redis����������ɾ���������³��õ�Redis����ָ�ͨ���Ը����Լ���Ӧ�ӿڵ��޸Ŀ���Ӱ�쵽����ʹ�ø�����`Asp.Net Core`
��⣬���ǵ������Խ��鿪��������ɾ�����������ӱ�������Ӷ�Ӱ��ҵ�񿪷���   

#### PoolRedisClient��
������Ҫʵ���˲�����ʵ���Ĺ�������Ӧ�Ը߲��������¶���Redis�Ŀ��飬��Ȼ������Ҫ������`RedisClient`����ʵ�ʵ�
ָ��ִ�еģ��������ǿ��Կ������������������`ConcurrentQueue`��`SemaphoreSlim`���й���   

#### XXXXCommands��
������Ҫ�Ǹ���Redisָ�����Ͻ��л��֣��Ӹ���Ŀ�п��Է�����Ҫʵ����`Connection`��`Hash`��`Key`��`List`��`Set`��`String`
�⼸����õ�Redis���ݽṹ��ͨ���Ĳ��ֿ��Թ۲����Redisָ���ƴ�ӡ�   

#### ReturnTypeWithXXX��   
������Ҫ�Ǹ���Redisָ��ķ������ͽ��л��ܣ���Ҫ��`XXXXCommands`��ʹ�ã�Ҳ��ʵ�ʴ洢��ƴ��Redisָ��Ķ���   

#### RedisConnector��   
�ײ㸺�����Ӻ�����ִ�����������࣬������ʹ����`AsyncConnector`�ฺ���첽������ִ�У�ͨ��`RedisIO`����ʵ�ʵ�
�����ֽڵķ�������ա�    

#### RedisIO��   
������Ҫ�����Socket���ķ�������գ�����ʹ��`RedisWriter`��`RedisReader`���л����ĵײ�RedisЭ���ת����������ա�    

### �����չ
����Redis�汾�ĸ���Խ��Խ�����ָ�����֣����ǵ����ֵ��������ĸ��½��ȵ����ƣ�Ϊ�˱��ڿ������ܹ����ٵ����н�����չ
���½�������ν���ָ��Ŀ�����չ������������Ҫ�����ĵ�ȷ����ָ��ķ������ݵ����ͽṹ��Ȼ���½���Ӧ��`XXXXCommands`�ļ�
Ȼ��������д���Ӧ�ķ���������Key��Del������
```
/// <summary>
/// ɾ��������һ������key�������ڵ�key������ԡ�
/// </summary>
/// <param name="keys">��Ҫɾ����key</param>
/// <returns>�������</returns>
public static ReturnTypeWithInt Del(params string[] keys)
{
	return new ReturnTypeWithInt("DEL", keys);
}
```
ͨ�����ϵķ�ʽ�Ϳ��Կ��ٵ�����һ���µķ���������Ӧ����Ҫ��`PoolRedisClient`�����н��й������������ǵĵ�Ԫ����
����ʵ��ʹ�ö��޷����ʣ��������ϵķ�����`PoolRedisClient`����д��
```
public long Del(params string[] keys) => Multi(KeyCommands.Del(keys));
```
���Կ������ǽ���ֻ����Ҫ����Ӧ��Commands�ķ�����ͨ��`Multi`�������뼴�ɡ������ͺ����׵���չ��һ���µ�Redisָ�   

### ����ʹ�ó���
1. ͨ��`SetNx`����ʵ�ּ򵥵ķֲ�ʽ����
2. ͨ��`Append`��`StrLen`��`GetRange`����ʵ��ʱ�����У�
3. ͨ��`BitCount`��`SetBit`��`GetBit`����ʵ��λͼ���ݣ�
4. ͨ��`Decr`��`DecrBy`��`Incr`��`IncrBy`����ʵ�ּ���������������
5. ͨ��`HDel`��`HExists`��`HGet`��`HLen`��`HSet`��`HSetNx`����ʵ���ڴ��ֵ䣻
6. ͨ��`BLPop`��`BRPop`��`LIndex`��`LLen`��`LPush`��`LPushX`��`RPop`��`RPush`��`RPushX`����ʵ���¼�����
7. ͨ��`BRPOPLPUSH`��`RPOPLPUSH`��`LRem`����ʵ�ְ�ȫ���к�ѭ���б�

#### ��ؾ����ĵ�
1. [�ۺ�����](http://www.redis.cn/articles.html)   
2. [������ŵ���Redisʵ�ֲַ�ʽ��](http://www.redis.cn/articles/20181020004.html)   
3. [֪��Redisƽ̨��չ���ݽ�֮·](https://mp.weixin.qq.com/s/YKJ-Y6EZevvMK8MX38xE3w)   
4. [Sessionһ���Լܹ����ʵ��](https://mp.weixin.qq.com/s/iTdHyODJ12RvTbe6MILg6Q)   
5. [Redis������ƹ淶����������](https://mp.weixin.qq.com/s/gw1X34vtiwRcEYgLbWp23w)   
6. [���ģcodis��Ⱥ��������ʵ��](https://mp.weixin.qq.com/s/O4AqVdibJWs2ivs6dhdClQ)   

   
### ע��
* �Ѿ�ʹ���ϰ汾��ע�⣬��ǰ�°��Ѿ������˶�����`IRedisCache`�ӿڣ�������ʵ��`Asp.Net Core`�Ľӿڡ�